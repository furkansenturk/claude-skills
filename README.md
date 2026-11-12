# claude-skills

**English** · [Türkçe](README.tr.md)

Skills I wrote for Claude Code and other AI agents that support `npx skills`.

## Skills

| Skill | What it does |
|---|---|
| [orchestration](skills/orchestration/SKILL.md) | Splits large work into independent lanes, runs them as parallel background subagents, verifies each result and combines them into one answer. For multi-component features, broad investigations and reviews. |
| [apple-design](skills/apple-design/SKILL.md) | Apple's design and UI coding standards in a platform-agnostic form: spacing, target sizes, typography, color and contrast, motion, component behavior, UX writing, input, app patterns, and how to implement them. For web, Flutter, React Native, Electron, Tauri and SwiftUI. |

## Structure

```
skills/                     standalone skills, one folder each
  orchestration/
    SKILL.md
  apple-design/
    SKILL.md
    references/             detailed rules, read on demand
.claude-plugin/
  marketplace.json          registers this repo as a Claude Code marketplace
  plugin.json               the "furkan-skills" plugin, bundling every skill under skills/
```

Each skill is a folder with a `SKILL.md` that starts with this frontmatter:

```markdown
---
name: skill-name           # required: same as the folder name; a-z, 0-9 and single hyphens; max 64 characters
description: What it does and when to use it.   # required: max 1024 characters
license: MIT               # optional
compatibility: Requires Python 3.               # optional, only for a special requirement (max 500 characters)
metadata:                  # optional, string → string
  author: furkansenturk
  version: "1.0.0"
---
```

The format follows the [Agent Skills specification](https://agentskills.io/specification). Keep `SKILL.md` under 500 lines. Long documents go in `references/`, helper scripts in `scripts/`, templates and data files in `assets/`. Paths are relative to the skill folder. Reference files over 100 lines start with a table of contents.

## Installation

### Option 1: `npx skills` (Claude Code, Cursor, Codex, etc.)

```bash
npx skills add furkansenturk/claude-skills                          # all skills
npx skills add furkansenturk/claude-skills --skill apple-design     # one skill
```

### Option 2: Claude Code plugin

```
/plugin marketplace add furkansenturk/claude-skills
/plugin install furkan-skills@claude-skills   # every skill under skills/
```

### Option 3: Manual

```bash
git clone https://github.com/furkansenturk/claude-skills
cp -r claude-skills/skills/* ~/.claude/skills/
```

## Adding a skill

1. Create a folder under `skills/` named after the skill and put a `SKILL.md` in it (frontmatter above).
2. Add it to the table above, in both `README.md` and `README.tr.md`.
3. Commit and push.

## License

[MIT](LICENSE).

The `apple-design` skill summarizes Apple's Human Interface Guidelines in its own words. It is not affiliated with or endorsed by Apple Inc. Apple and related names are trademarks of Apple Inc.
