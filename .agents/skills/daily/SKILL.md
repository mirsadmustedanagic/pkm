---
name: daily
description: Create career-focused daily notes and run the Morning Setup + Afternoon Review routines. Use for daily engineering planning and end-of-day capture.
allowed-tools: Read, Write, Edit, Glob, Grep, TaskCreate, TaskUpdate, TaskList, TaskGet
user-invocable: true
---

# Daily Workflow Skill

Creates career-focused daily notes and provides structured Morning Setup (5 min) and Afternoon Review (5 min) routines.

The vault is career-only. This skill does NOT track gratitude, energy scores, or personal-life tasks.

## Usage

Invoke with `/daily` or ask Claude to create today's note or run a routine.

### Create Today's Note
```
/daily
```

Or ask:
- "Create today's daily note"
- "Start morning setup"
- "Run afternoon review"

## Daily Note Creation

### What Happens
1. **Check if today's note exists** in `Daily Notes/YYYY-MM-DD.md`
   - If yes: open it
   - If no: create it from `Templates/Daily Note - Career.md`

2. **Template processing** — replace `{{date}}`, `{{date:format}}`, `{{date-1:YYYY-MM-DD}}`, `{{date+1:YYYY-MM-DD}}`.

3. **Ask the user to pick the primary project for today.**
   - Options: `netilion2` (default), `netilion-monorepo`, other
   - Write it into the "Primary project today" line.

### Template Variables
- `{{date}}`, `{{date:dddd}}`, `{{date:MMMM DD, YYYY}}`
- `{{date-1:YYYY-MM-DD}}` / `{{date+1:YYYY-MM-DD}}`
- `{{time}}`

## Morning Setup (5 min)

### Automated Steps
1. Create today's daily note (if missing) from `Templates/Daily Note - Career.md`.
2. Pull incomplete tasks from yesterday's note into the "Yesterday's incomplete" list.
3. Surface current focus context:
   - This month's priority from `Goals/2. Monthly Goals (Current).md`
   - Active project current focus from `Projects/netilion2/CLAUDE.md` and `Projects/netilion-monorepo/CLAUDE.md`
4. Prompt user to confirm the primary project and set a deep-work block.

### Context Block to Surface

```markdown
### Today's Context
- **Monthly focus:** [from Goals/2. Monthly Goals (Current).md]
- **netilion2 current focus:** [Current Focus section]
- **netilion-monorepo:** [Current Focus section — maintenance mode]
```

### Interactive Prompts
- "What's the ONE Big Thing to ship today?"
- "Which project is primary — netilion2, netilion-monorepo, or other?"
- "When is your protected deep-work block?"

### Task Tagging
When adding tasks, tag them by project or type:

```markdown
- [ ] Wire up auth middleware #project/netilion2
- [ ] Bump lockfile in monorepo #project/netilion-monorepo
- [ ] Investigate ORM caching bug #learning
```

### Morning Checklist
- [ ] Daily note created from `Daily Note - Career.md`
- [ ] Primary project selected
- [ ] Monthly + project focus reviewed
- [ ] Yesterday's incomplete tasks carried forward
- [ ] ONE Big Thing identified
- [ ] Deep-work block scheduled

## Afternoon Review (5 min)

Run at end of workday. Fill in the "Afternoon Review" section of the daily note.

### Capture
1. **What did I ship today?** — concrete shipped items (PRs, features, decisions, docs).
2. **What blocked me?** — anything that stalled progress; tag with `#blocker`.
3. **One decision or learning to log?** — if yes, add a row to the relevant project's `Decisions & Learnings` table in `Projects/<name>/CLAUDE.md`.
4. **Next highest priority for tomorrow.**
5. **Deep work actual vs planned** (hours).
6. **Primary project stayed?** (Y/N + why if not).

### Decision Capture Guidance
When a decision or learning is logged, write it directly into the project CLAUDE.md's Decisions & Learnings table:

```markdown
| 2026-07-21 | Switched from X to Y | Perf: 40% faster; tradeoff: more memory | Adopted for all endpoints |
```

Also tag with `#decision` in the daily note for later search.

### Afternoon Checklist
- [ ] Shipped items captured
- [ ] Blockers noted (tagged `#blocker`)
- [ ] Decision/learning logged in project CLAUDE.md (if any)
- [ ] Tomorrow's top priority set
- [ ] Deep-work hours recorded
- [ ] `/push` run to commit

## Task-Based Progress Tracking

The daily skill uses session tasks to show progress during routines. Session tasks are temporary spinners — the real record lives in the daily note and project CLAUDE.md files.

### Morning Setup Tasks

```
TaskCreate:
  subject: "Create daily note"
  activeForm: "Creating daily note from career template..."

TaskCreate:
  subject: "Pull incomplete tasks"
  activeForm: "Pulling incomplete tasks from yesterday..."

TaskCreate:
  subject: "Surface monthly + project focus"
  activeForm: "Surfacing monthly and project focus..."

TaskCreate:
  subject: "Set deep-work block"
  activeForm: "Confirming deep-work block..."
```

Chain with `addBlockedBy` so each task waits on the previous. Mark `in_progress` on start, `completed` on finish.

### Afternoon Review Tasks

```
TaskCreate:
  subject: "Capture shipped + blockers"
  activeForm: "Capturing shipped items and blockers..."

TaskCreate:
  subject: "Log decision/learning"
  activeForm: "Logging decision to project CLAUDE.md..."

TaskCreate:
  subject: "Set tomorrow's priority"
  activeForm: "Setting tomorrow's priority..."
```

## Configuration

- Daily notes folder: `Daily Notes/`
- Template: `Templates/Daily Note - Career.md`
- Date format: `YYYY-MM-DD`

## Integration

Works with:
- `/push` — commit after Afternoon Review
- `/weekly` — Friday per-project review consumes daily notes
- `/monthly` — rolls up daily decisions and shipped items
- `/project` — project CLAUDE.md files receive decision log rows
- `/onboard` — load context before Morning Setup
