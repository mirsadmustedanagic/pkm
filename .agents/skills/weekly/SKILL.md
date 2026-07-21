---
name: weekly
description: Friday per-project weekly review. Iterates over active projects (netilion2, netilion-monorepo), captures shipped/blockers/decisions, plans next week. Budget ~15 min per project.
allowed-tools: Read, Write, Edit, Glob, Grep, TaskCreate, TaskUpdate, TaskList, TaskGet
user-invocable: true
---

# Weekly Review Skill

Runs a Friday per-project weekly review. One review note per active project using `Templates/Weekly Project Review.md`. Budget ~15 min per project.

Career-only. No life-area sections, no habit tracking, no gratitude.

## Usage

```
/weekly
```

Or ask:
- "Run my Friday weekly review"
- "Weekly review for netilion2"

## What This Skill Does

1. **Identifies active projects** by scanning `Projects/*/CLAUDE.md`.
   - Primary: `netilion2` (active).
   - Secondary: `netilion-monorepo` (maintenance mode — lighter review).
2. **For each active project**, creates a weekly review note from `Templates/Weekly Project Review.md`.
3. **Guides per-project reflection** (≤ 15 min): shipped, in progress, blockers, decisions/learnings, next week priorities.
4. **Rolls decisions/learnings up** into each project's `Decisions & Learnings` table in `Projects/<name>/CLAUDE.md`.
5. **Updates monthly rollup**: appends key wins and decisions to `Goals/2. Monthly Goals (Current).md`.

## Where Review Notes Live

Save weekly review notes to `Projects/<project>/Weekly Reviews/YYYY-MM-DD.md` (create the subdirectory if missing).

## Per-Project Review Steps (≤15 min each)

Repeat for each active project (netilion2, then netilion-monorepo):

### Step 1: Collect (5 min)
- Read daily notes from the past 7 days, filter for `#project/<name>` tags.
- Extract shipped items, blockers (`#blocker`), decisions (`#decision`).
- Read `Projects/<name>/CLAUDE.md` for current focus + existing blockers.

### Step 2: Reflect (5 min)
Fill in the template sections:
- Completed This Week
- In Progress
- Blockers (severity, owner, next step — escalate if >2 weeks old)
- Velocity Notes (PRs merged, features shipped, deep-work hours)
- Decisions or Learnings to Log

### Step 3: Plan (5 min)
- 3 priorities for next week
- Any escalations or scope adjustments
- Update `Projects/<name>/CLAUDE.md`:
  - Refresh "Current Focus"
  - Append this week's row to "Weekly Progress Notes"
  - Add any new rows to "Decisions & Learnings"

## Monthly Rollup Step (once, after all projects reviewed)

- Append a short bullet summary to `Goals/2. Monthly Goals (Current).md` under this month's log:
  - Key decisions logged this week (with project prefix)
  - Any blockers escalated
  - Deep-work % achieved vs target

## Interactive Prompts (per project)

1. "What did you ship for <project> this week?"
2. "What blocked you? Anything to escalate?"
3. "Any decision or learning worth capturing in the project's decision log?"
4. "Top 3 priorities for <project> next week?"

## Weekly Review Checklist

- [ ] netilion2 review note created and filled
- [ ] netilion-monorepo review note created and filled (lighter — maintenance mode)
- [ ] Decisions & Learnings rows added to project CLAUDE.md files
- [ ] Blockers >2 weeks old flagged
- [ ] Next week priorities set per project
- [ ] Monthly rollup updated
- [ ] `/push` run to commit

## Task-Based Progress Tracking

Use session tasks to make the multi-project flow visible.

```
TaskCreate:
  subject: "Scan active projects"
  activeForm: "Scanning Projects/*/CLAUDE.md..."

TaskCreate:
  subject: "Review netilion2"
  activeForm: "Running netilion2 weekly review..."

TaskCreate:
  subject: "Review netilion-monorepo"
  activeForm: "Running netilion-monorepo weekly review..."

TaskCreate:
  subject: "Roll up to monthly"
  activeForm: "Rolling decisions into monthly log..."
```

Chain with `addBlockedBy`. Mark `in_progress` at the start of each project, `completed` when its review note and CLAUDE.md updates are saved.

## Timing

- Run every Friday afternoon.
- Total time: ~15 min × N active projects + 5 min rollup.

## Integration

Works with:
- `/daily` — provides source material (tagged tasks, decisions, blockers)
- `/monthly` — consumes weekly rollups
- `/project` — updates project CLAUDE.md files
- `/push` — commit after review
