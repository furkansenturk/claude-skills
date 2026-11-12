---
name: orchestration
description: Split large work into independent lanes, run them as parallel background subagents, verify each result, and synthesize one answer. Use for multi-component features, broad investigations, or reviews that benefit from parallel workers.
license: MIT
metadata:
  author: furkansenturk
  version: "1.0.0"
---

# Orchestration

You coordinate: decompose, delegate, verify, synthesize. Workers do the bulk reading and editing. Your context is the scarce resource; protect it.

Orchestration is not a way to save tokens on small work. Every worker pays a fresh start (system prompt, tool schemas, re-discovery) of roughly 15k tokens before it does anything. It pays off only when solo work would push your own context past ~80k tokens, because you then re-send that context on every tool call, or when a cheap model can do a lane a strong model would otherwise do.

## Gate: orchestrate or go solo

Orchestrate only when all three hold:
1. The work splits into ≥2 lanes that can run without each other's output.
2. Each lane would cost you ≥15 tool calls or ≥10 file reads solo. Below that, briefing and verifying cost more than doing.
3. You can state a check for each lane that one command can answer.

Otherwise do it yourself. Always solo: one-file edits, live-state debugging, anything needing the user mid-task, anything you have already half-read into context.

## Plan (before any spawn)

Write a lane table and show it to the user in ≤10 lines. No prose around it.

```
| lane | deliverable | agent/model | files it owns | done when |
```

How to cut lanes:
- Cut along verification boundaries, not layers. A lane is right when one command proves it alone. "Backend" and "frontend" of the same feature are a bad cut; "the API endpoint with its tests" and "the migration with its tests" are a good cut.
- If two lanes would share an interface (type, schema, function signature, API shape), write that interface yourself first, in a wave of its own or solo. Never let two workers guess the same contract.
- Each lane: one deliverable, disjoint files. Shared files (index/barrel files, package.json, lockfiles, migrations, config) belong to no lane; you edit them after the wave.
- Dependent lanes go to the next wave. Do not start a wave until the previous one is verified. Max 4 lanes per wave, max 3 waves. More than that: narrow the scope or ask.
- For review or investigation lanes, give the question and the code, not your hypothesis. A worker handed a hypothesis returns it confirmed.
- Ask the user only when the code cannot answer the question. Ask everything in one message, before the first spawn.

## Agent and model choice

| lane type | agent | model |
|---|---|---|
| find / read / map code, no edits | `Explore` | haiku |
| mechanical edits with a clear pattern (rename, add field, port tests) | `general-purpose` | haiku or sonnet |
| feature code, refactor, bug fix | `general-purpose` | sonnet |
| design judgment, ambiguous spec, cross-cutting change | `general-purpose` | opus |

Spawn the whole wave in one message with `run_in_background: true`. Use `isolation: "worktree"` when two lanes must touch the same files or a lane runs tests that write to disk.

Use `subagent_type: "fork"` only when a lane needs most of what you have already read; it copies your whole context, so it is the most expensive start. Otherwise spawn fresh and put the few facts it needs in CONTEXT.

## Worker brief

Start every prompt with this. Point to files; never paste their contents.

```text
=== WORKER AGENT ===
You are a worker, not an orchestrator.
- Complete only the task below. Do not spawn subagents.
- Do not commit, push, or run the full build unless the task says to.
- Do not edit files outside SCOPE. If you must, stop and report why.
- If CONTEXT or TASK contradicts what you find in the code, stop and report the contradiction. Do not force the plan.
- Search before you read: Grep/Glob to locate, then Read only the line ranges you need.
- Budget: <N> tool calls. If you are not converging by then, stop and report BLOCKED with what you learned.
- Run DONE WHEN yourself before reporting. If it fails, report BLOCKED. Never write VERIFIED for a check you did not run.
- Final report, ≤150 words, in this exact shape:
  CHANGED: <file paths, one line each with what changed>
  VERIFIED: <the command you ran and its result>
  BLOCKED: <what you could not do, or "none">
  Do not include file contents or diffs in the report.
====================

GOAL: <one sentence: what the whole job is for, so the worker can make local calls the brief did not anticipate>
TASK: <one deliverable>
CONTEXT: <file paths and facts the worker needs; include anything you already learned so it is not re-discovered>
SCOPE: may touch <paths>. Must not touch <paths>.
DONE WHEN: <a command or grep that proves it, e.g. `npm test -- auth` passes; `grep -r OldName src/` returns nothing>
```

For read-only lanes (find, map, review, investigate) replace the report shape with:

```text
FINDINGS: <≤10 items, each one line, each with file:line>
CONFIDENT: <which findings you verified by reading the code path end to end>
UNSURE: <which findings are inference, and what would settle them>
NOT COVERED: <what the task asked that you could not reach>
```

Budget guide: 15 tool calls for a mechanical lane, 30 for a feature lane, 40 for an investigation. Set it lower if the lane is small.

## Verify

Do not trust the report. For each lane run the DONE WHEN check yourself; that is one command, so it is cheap. Read a diff only if the check fails or `git diff --stat` shows a file outside the lane's SCOPE. Do not re-read files the worker summarized.

On failure, first decide whose fault it is:
- The worker reported a contradiction, or the failure shows your CONTEXT or SCOPE was wrong: fix the brief. Do not retry the same brief.
- Small fix, same cause: `SendMessage` to the same worker with only the failure output. Its context is already loaded.
- Wrong approach, or second failure: spawn a fresh worker with the corrected brief plus the failure output. Do not forward the prior worker's report.
- Third failure: mark the lane blocked and move on. Do not finish it yourself unless it is under 5 tool calls.

## Close

For code changes:
1. Edit the shared files you reserved.
2. Run the whole-project build, lint, and tests once. Never inside parallel workers.
3. Report in this shape, nothing else:
   - **Changed:** file paths grouped by lane.
   - **Verified:** which checks ran and their results.
   - **Open:** blocked lanes with the last failure, skipped items, anything the user must decide.

For investigations and reviews:
1. Where two lanes disagree, open the file:line both cite and decide. Do not report both.
2. Keep each finding's file:line. Drop findings that are UNSURE unless you checked them yourself.
3. Report what no lane covered as a gap, not as "no issues found".
4. Answer the user's question in the first paragraph. Evidence after.

Never say done while Open or a gap is non-empty.
