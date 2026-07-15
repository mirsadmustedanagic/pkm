# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

# Obsidian PKM Vault Context

## System Purpose
Build meaningful work and growth across career, health, relationships, and personal development while maintaining balance and intentional progress.

## Directory Structure

| Folder | Purpose |
|--------|---------|
| `Daily Notes/` | Daily journal entries (`YYYY-MM-DD.md`) |
| `Goals/` | Goal cascade (3-year → yearly → monthly → weekly) |
| `Projects/` | Active projects with their own `CLAUDE.md` |
| `Templates/` | Reusable note structures |
| `Archives/` | Completed/inactive content |
| `Inbox/` | Uncategorized captures (optional) |

## Current Focus

**Primary Areas:** Career & Professional, Health & Wellness, Relationships, Personal Growth

See [2. Monthly Goals.md](Goals/2.%20Monthly%20Goals.md) for this month's priorities.

## Tag System

**Priority:** `#priority/high`, `#priority/medium`, `#priority/low`
**Status:** `#active`, `#waiting`, `#completed`, `#archived`
**Context:** `#work`, `#personal`, `#health`, `#learning`, `#family`

## Available Skills

Skills are invoked with `/skill-name` or automatically by Claude when relevant.

| Skill | Invocation | Purpose |
|-------|------------|---------|
| `daily` | `/daily` | Create daily notes, morning/midday/evening routines |
| `weekly` | `/weekly` | Run weekly review, reflect and plan |
| `monthly` | `/monthly` | Monthly review, quarterly milestone check, next month planning |
| `project` | `/project` | Create, track, and archive projects linked to goals |
| `review` | `/review` | Smart router — auto-detects daily/weekly/monthly based on context |
| `push` | `/push` | Commit and push changes to Git |
| `onboard` | `/onboard` | Interactive setup (first run) + load vault context |
| `adopt` | `/adopt` | Scaffold PKM system onto an existing Obsidian vault |
| `upgrade` | `/upgrade` | Update to latest version, preserving your content |
| `goal-tracking` | (auto) | Track progress across goal cascade with project awareness |
| `obsidian-vault-ops` | (auto) | Read/write vault files, manage wiki-links |

### Progress Visibility

Skills and agents use session task tools to show progress during multi-step operations:

```
[Spinner] Creating daily note...
[Spinner] Pulling incomplete tasks...
[Done] Morning routine complete (4/4 tasks)
```

Session tasks are temporary progress indicators—your actual to-do items remain as markdown checkboxes in daily notes.

## Available Agents

| Agent | Purpose |
|-------|---------|
| `note-organizer` | Organize vault, fix links, consolidate notes |
| `weekly-reviewer` | Facilitate weekly review aligned with goals |
| `goal-aligner` | Check daily/weekly alignment with long-term goals |
| `inbox-processor` | GTD-style inbox processing |

## Output Styles

**Productivity Coach** (`/output-style coach`)
- Challenges assumptions constructively
- Holds you accountable to commitments
- Asks powerful questions for clarity
- Connects daily work to mission

## The Cascade

The full goals-to-tasks flow:

```
3-Year Vision  →  Yearly Goals  →  Projects  →  Monthly Goals  →  Weekly Review  →  Daily Tasks
   /goal-tracking     /project        /project      /monthly          /weekly         /daily
```

## Daily Workflow

### Morning (5 min)
1. Run `/daily` to create today's note
2. Review cascade context (ONE Big Thing, project next-actions)
3. Identify ONE main focus
4. Review yesterday's incomplete tasks
5. Set time blocks

### Evening (5 min)
1. Complete reflection section
2. Review goal/project attention summary
3. Move unfinished tasks
4. Run `/push` to save changes

### Weekly (30 min - Sunday)
1. Run `/weekly` for guided review
2. Review project progress table
3. Calculate goal progress
4. Plan next week's focus
5. Archive old notes

### Monthly (30 min - End of month)
1. Run `/monthly` for guided review
2. Roll up weekly wins/challenges
3. Check quarterly milestones
4. Plan next month's focus

## Best Practices

1. **Be Specific** - Give clear context about what you need
2. **Reference Goals** - Connect daily tasks to objectives
3. **Use Coach Mode** - When you need accountability
4. **Keep It Current** - Update project CLAUDE.md files regularly

## System Architecture

### Directory Layout
```
.claude/
├── skills/              # Invocable skills (e.g., /daily, /weekly, /project)
├── agents/              # Custom agents (goal-aligner, note-organizer, etc.)
├── rules/               # Vault conventions (markdown standards, task tracking)
├── output-styles/       # Display modes (e.g., coach mode)
├── hooks/               # Git hooks for automation
├── scripts/             # Utility scripts
└── settings.json        # Harness configuration
```

### How Skills Work
Skills like `/daily`, `/weekly`, `/project` are self-contained tools in `.claude/skills/`. Each has a `SKILL.md` defining its behavior. Skills use **session tasks** (temporary progress spinners) for multi-step operations—these are separate from the markdown checkboxes that persist your actual to-do items.

### Rules & Conventions
The `.claude/rules/` directory contains governance:
- **markdown-standards.md** — File naming, heading structure, frontmatter format, tags
- **task-tracking.md** — When/how to use session tasks vs. real markdown tasks
- **project-management.md** — Project structure and lifecycle
- **productivity-workflow.md** — Daily/weekly/monthly rituals

## Common Operations

### Saving Changes
Use the `/push` skill to commit and push:
```
/push
```
Or manually:
```bash
git add .
git commit -m "Your message"
git push origin main
```

### Running Skills
Skills are invoked with `/` prefix in chat:
- `/daily` — Create today's note
- `/weekly` — Weekly review (run Sundays)
- `/monthly` — Monthly review (run at month end)
- `/review` — Smart router (auto-detects daily/weekly/monthly)
- `/project` — Create/track projects
- `/onboard` — Interactive setup + load context

### Memory System
Claude remembers context across conversations via `/.claude/projects/-Users-mirsad-dev-PKM/memory/`. When relevant, previous context is recalled automatically. See `memory/MEMORY.md` for the index.

## Customization

### Adding Custom Agents
Create agents in `.claude/agents/` with `<name>.md`. Follow the structure of existing agents (goal-aligner, note-organizer, etc.).

### Adding Hooks
Git hooks live in `.claude/hooks/`. Configure in `.claude/settings.json` to trigger on events like `pre-commit`, `post-merge`, etc.

### Adding Output Styles
New display modes go in `.claude/output-styles/` as markdown files with clear instructions.

### Local Overrides
For personal settings that shouldn't be committed, create `CLAUDE.local.md`.
See `CLAUDE.local.md.template` for format.

---

*Last Updated: 2026-07-14*
*System Version: 3.1*


<claude-mem-context>
# Recent Activity

<!-- This section is auto-generated by claude-mem. Edit content outside the tags. -->

*No recent activity*
</claude-mem-context>