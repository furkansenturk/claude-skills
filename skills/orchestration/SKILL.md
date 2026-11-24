---
name: orchestration
description: Splits large work into independent lanes, runs them as parallel background subagents, verifies each result, and synthesizes one answer. Use for large multi-component features, broad investigations, reviews, or bulk data jobs that benefit from parallel subagents, or when asked to orchestrate, parallelize, or fan out work. 
license: MIT
metadata:
  author: furkansenturk
  version: "1.1.0"
---

# Orchestration

You coordinate: decompose, delegate, verify, synthesize. Workers do the bulk reading and editing. Your context is the scarce resource; protect it.

Orchestration is not a way to save tokens on small work: every worker pays a fixed start-up cost (system prompt, tool schemas, re-discovering the code) before it does anything.

## Gate: orchestrate or go solo

Orchestrate only when all three hold:
1. The work splits into ≥2 lanes that can run without each other's output.
2. Each lane would cost you ≥15 tool calls or ≥10 file reads solo.
3. You can say how you will check each lane: one command for a lane that changes things, file:line evidence you can open for a read-only lane.

If you cannot judge these without reading the code, send one `Explore` lane to map it, then apply the gate and cut lanes from its report. Do not fill your own context to decide.

Otherwise do it yourself. Always solo: one-file edits, live-state debugging, anything needing the user mid-task, a job you have already mostly read.

## Plan (before any spawn)

Write a lane table, one row per lane, and show it to the user with no prose around it, then proceed without waiting for approval.

```
| lane | deliverable | agent/model | files it owns | after | done when |
```

How to cut lanes:
- Cut along verification boundaries, not layers. A lane is right when one command proves it alone. "Backend" and "frontend" of the same feature are a bad cut; "the API endpoint with its tests" and "the email sender with its tests" are a good cut.
- If two lanes would share an interface (type, schema, function signature, API shape), write that interface yourself first, including what it returns or throws on failure and on empty input, before the lanes that use it, or solo. Never let two workers guess the same contract.
- Each lane: one deliverable, disjoint files to edit. Files more than one lane would edit (index/barrel files, package.json, lockfiles, config) belong to no lane: edit them yourself, before the lane starts if its check needs the change, otherwise after.
- When several lanes apply the same brief to different inputs, run one first, verify it, fix the brief, then spawn the rest. The pilot does not count toward the lane limit.
- Bulk data (normalize, dedupe, classify, extract): you decide the rules, never the worker. Deterministic rules: write one script and run it over everything, no worker per batch. Per-item judgment: batches small enough that a bad one is cheap to redo, each writing its own output file; sample before merging, and run cross-batch steps (such as dedupe) once, by script, after the merge.
- A lane that needs another lane's output names it in `after` and starts only once that lane is verified; lanes with nothing to wait for start together. Do not spawn a lane whose `after` is still unverified. Max 4 lanes running at once, max 12 lanes in all. More than that: narrow the scope or ask.
- For review or investigation lanes, give the question and the code, not your hypothesis. A worker handed a hypothesis returns it confirmed; to test one, ask for the evidence that would rule it out. Cut investigations by question, not by module: a cause that crosses modules is missed by lanes that each own one. Ask a root-cause lane for the command that reproduces the failure.
- Ask the user only when the code cannot answer the question. Ask everything in one message, before the first spawn.

## Agent and model choice

| lane type | agent | model | effort |
|---|---|---|---|
| find / map code, no edits | `Explore` | haiku | low |
| mechanical edits with a clear pattern (rename, add field, port tests) | `general-purpose` | haiku or sonnet | low |
| bulk data cleanup | `general-purpose` | haiku | low |
| feature code, refactor, bug fix | `general-purpose` | sonnet | medium |
| review, bug hunt, root cause (read-only by SCOPE) | `general-purpose` | sonnet | high |
| design judgment, ambiguous spec, cross-cutting change | `general-purpose` | opus | high |

Set `model` and `effort` explicitly on every spawn. Left out, a worker can end up on your model, the most expensive tier. When unsure between two models for a lane that a command checks, take the cheaper one; the check catches a miss. A read-only lane has no such net, so do not go below the table.

`Explore` cannot judge code or write files; review lanes and lanes with an output file need `general-purpose`.

Spawn every lane that is ready in one message. While they run, do not poll workers or read their partial output; you are notified as each finishes. Prepare the briefs of waiting lanes instead. Stop a worker as soon as another lane's result makes it unnecessary.

Use `isolation: "worktree"` only when parallel lanes' tests or builds would overwrite each other's output on disk. A worktree starts from the default branch, so it lacks your branch's commits and all uncommitted work (earlier lanes, files you edited); never use it for a lane that needs any of that; afterwards apply each worktree's diff to the main tree one lane at a time and rerun that lane's check.

Use `subagent_type: "fork"` only when one lane of a larger job needs most of what you have already read. It reuses your context instead of re-discovering it, but always runs on your model; `model` and `effort` are ignored. Otherwise spawn fresh and put the few facts the lane needs in CONTEXT.

## Worker brief

Start every prompt with this. Point to files; never paste their contents. When several lanes share a brief or facts, write them to one file and point each prompt to it.

```text
=== WORKER AGENT ===
You are a worker, not an orchestrator.
- Complete only the task below. Do not spawn subagents.
- Do not commit, push, or run the full build unless the task says to.
- Do not edit files outside SCOPE. If you must, stop and report why.
- If CONTEXT or TASK contradicts what you find in the code, stop and report the contradiction.
- Search before you read: Grep/Glob to locate, then Read only the line ranges you need.
- Budget: <N> tool calls. If you are not converging by then, stop and report BLOCKED with what you learned.
- Do not change, skip, or weaken existing tests or the DONE WHEN check to make it pass.
- Run DONE WHEN yourself before reporting; if it still fails when you stop, report BLOCKED. Never write VERIFIED for a check you did not run.
- Final report, ≤150 words, in this exact shape:
  CHANGED: <file paths, one line each with what changed>
  VERIFIED: <the command you ran and its result>
  BLOCKED: <what you could not do, or "none">
  LEARNED: <facts the next worker would otherwise re-discover: commands, conventions, traps; or "none">
  Do not include file contents or diffs in the report.
====================

GOAL: <one sentence: what the whole job is for, so the worker can make local calls the brief did not anticipate>
TASK: <one deliverable>
CONTEXT: <file paths and facts the worker needs, including, for lanes that write code, one existing file whose patterns to follow (the same one for similar lanes); include anything you already learned>
SCOPE: may touch <paths>. Must not touch <paths>.
DONE WHEN: <a command or grep that proves it, e.g. `npm test -- auth` passes; `grep -r OldName src/` returns nothing>
```

Make DONE WHEN run the area's existing tests too, and print only failures and a summary line (full output to a log file).

For read-only lanes (find, map, review, investigate) drop DONE WHEN and the header lines that mention it, set SCOPE to read-only, and replace the report shape with the one below. The word cap does not apply to it; the ban on file contents does.

```text
FINDINGS: <≤10 lines, most important first, one finding per line with file:line; if you found more, end with one line saying how many were left out>
CONFIDENT: <which findings you verified by reading the code path end to end>
UNSURE: <which findings are inference, and what would settle them>
NOT COVERED: <what the task asked that you could not reach>
```

When a lane has more to return than the report holds, name an output file in SCOPE and have the worker write the rest there and return the path. Later lanes read that file directly; you read only the parts you need.

Match brief tightness to the model. For opus, state the goal, constraints and DONE WHEN, and leave the route to it; over-specifying removes the judgment you pay for. For sonnet, add the steps in order when order matters and say when to stop and report instead of improvising. For haiku, give the exact rules with 2–3 input and output examples.

Budget guide: 15 tool calls for a mechanical lane, 30 for a feature lane, 40 for an investigation.

## Verify

Do not trust the report.

- Lanes that change things: run the DONE WHEN check yourself. Read a diff only if the check fails, `git diff --stat` shows a file outside the lane's SCOPE, or the lane changed existing tests or the check itself: a weakened check proves nothing. Do not re-read files the worker summarized.
- Read-only lanes: open the file:line of the findings your answer will depend on most. Treat the rest as reported, not verified. For a root-cause lane, run its reproduction command yourself; only a run you saw counts.

Put each report's LEARNED facts into the CONTEXT of lanes that have not started yet. If a report shows the plan was wrong (two lanes needed the same file, two lanes did the same reading, a lane turned out trivial or unnecessary), recut the lanes that have not started before spawning more; do not run a plan you know is wrong to the end.

On failure, first decide whose fault it is:
- A check fails in a way the lane's own files do not explain, in the worker's run or your rerun: first rule out the environment (a sibling lane's unfinished edits, worktree, working directory, reserved files not yet edited). That is not a lane failure.
- The worker reported a contradiction, or the failure shows your CONTEXT or SCOPE was wrong: fix the brief. Do not retry the same brief.
- First failure with a small fix: `SendMessage` to the same worker with only the failure output.
- Wrong approach, or a lane's second failure: spawn a fresh worker with the corrected brief plus the failure output, and say that the first attempt is still in the files. If the brief was right and the model fell short, move one model tier up. Do not forward the prior worker's report.
- A lane's third failure: mark it blocked and move on; lanes that depend on it are skipped and go to Open. Do not finish it yourself unless it is under 5 tool calls.

## Close

For code or data changes:
1. Edit the shared files you reserved.
2. For code, read the lanes' combined diff once, tests included, for duplication across lanes, dead code, departures from the reference file's patterns, and new tests that would pass without the change. Fix small things yourself; send larger ones back as a lane failure.
3. Run the whole-project build, lint, and tests once. If nothing exercises the lanes together, run one check that does.
4. Report in this shape, nothing else:
   - **Changed:** file paths grouped by lane.
   - **Verified:** which checks ran and their results.
   - **Open:** blocked lanes with the last failure, skipped items, anything the user must decide.

For investigations and reviews:
1. Where two lanes disagree, open the file:line both cite and decide. If the code does not settle it, report it as open, not as both.
2. Keep each finding's file:line. List findings you did not check yourself separately, marked unverified; never mix them into the answer.
3. Report what no lane covered as a gap, not as "no issues found".
4. For a root cause, name the run that reproduces the failure; without one, call it the likeliest cause, not the cause.
5. Answer the user's question in the first paragraph. Evidence after.

Never report the job as complete while Open or a gap is non-empty; report it as partial and say what remains.
