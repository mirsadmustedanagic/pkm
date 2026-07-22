---
name: monthly
description: Career-only monthly review. Roll up weekly project reviews, check quarterly milestones, plan next month's project focus.
allowed-tools: Read, Write, Edit, Glob, Grep, TaskCreate, TaskUpdate, TaskList, TaskGet
model: sonnet
user-invocable: true
---

# Monthly Review Skill

Facilitates the career-only monthly review: project momentum, decisions captured, deep-work % achieved, next month's project focus.

No life-area sections (no health, relationships, creativity, financial wellbeing scores).

## Usage

```
/monthly
```

Or ask:
- "Run my monthly review"
- "Plan next month's project focus"

## What This Skill Does

1. **Opens or creates** the monthly review section in `Goals/2. Monthly Goals (Current).md`.
2. **Rolls up weekly project reviews** from the past ~4 weeks.
3. **Checks quarterly milestones** in `Goals/1. Yearly Goals (2026 - RECLAIM).md`.
4. **Plans next month's project focus** and deep-work targets.

## Review Process

### Phase 1: Collect Monthly Data (10 min)

Read:
- `Goals/2. Monthly Goals (Current).md` — this month's plan and running log.
- Weekly project reviews for the month: `Projects/*/Weekly Reviews/*.md`.
- `Projects/netilion2/CLAUDE.md` and `Projects/netilion-monorepo/CLAUDE.md` — current focus, Weekly Progress Notes, Decisions & Learnings.
- Daily notes from the past ~30 days for `#decision` and `#blocker` tags.

Extract per project:
- Features/PRs shipped
- Decisions captured (count and highlights)
- Blockers (resolved vs still open)
- Deep-work hours vs target

### Phase 2: Reflect (10 min)

- Read `Goals/1. Yearly Goals (2026 - RECLAIM).md`. Identify the current quarter and its milestones.
- Assess quarterly milestone progress (on track / at risk / off track).
- Analyze patterns: primary project drift, blocker recurrence, decision velocity.
- Compare planned vs actual project focus and deep-work %.

### Phase 3: Plan Next Month (10 min)

- Set next month's ONE primary project focus.
- Define next month's deep-work % target.
- Identify 3–5 top project deliverables (per active project).
- Note any project phase transitions (Discovery → Build → Stabilize → Maintain).
- Update `Goals/2. Monthly Goals (Current).md` in place.

## Output Format

Append to `Goals/2. Monthly Goals (Current).md`:

```markdown
## Monthly Review: [Month YYYY]

### Summary
- Weeks reviewed: [N]
- Active projects: netilion2, netilion-monorepo
- Decisions captured: [N] (netilion2: [N], monorepo: [N])
- Deep-work % achieved: [X%] (target: [Y%])

### Project Momentum
| Project | Shipped | Decisions | Blockers open | Phase |
|---------|---------|-----------|---------------|-------|
| netilion2 |  |  |  |  |
| netilion-monorepo |  |  |  |  |

### Highlights
- [Top shipped items]

### Key Decisions Logged
- [Date | Project | Decision]

### Blockers
- [Still open — owner / next step]

### Quarterly Milestone Check (Q[N])
| Milestone | Status | Notes |
|-----------|--------|-------|
|  |  |  |

### Next Month Plan
**Primary project:** [netilion2 | netilion-monorepo]
**Deep-work target:** [X hours/week or Y%]

**Top deliverables:**
1.
2.
3.

**Phase transitions / scope changes:**
-

### Questions
- What single deliverable would make next month feel like a win?
- What decision is overdue?
- Which blocker needs escalation?
```

## Data Sources

Always read:
- `Goals/0. Three Year Vision (Career).md` — vision context
- `Goals/1. Yearly Goals (2026 - RECLAIM).md` — quarterly milestones
- `Goals/2. Monthly Goals (Current).md` — current plan (read and update)
- `Projects/*/CLAUDE.md` — project state
- `Projects/*/Weekly Reviews/*.md` — weekly rollups
- `Daily Notes/*.md` — past ~30 days for tag scan

## Task-Based Progress Tracking

```
TaskCreate:
  subject: "Phase 1: Collect monthly data"
  activeForm: "Collecting weekly reviews, project state, and tags..."

TaskCreate:
  subject: "Phase 2: Reflect + quarterly check"
  activeForm: "Reflecting on patterns and quarterly milestones..."

TaskCreate:
  subject: "Phase 3: Plan next month"
  activeForm: "Planning next month's project focus..."

TaskCreate:
  subject: "Write monthly review section"
  activeForm: "Appending monthly review to Goals/2. Monthly Goals (Current).md..."
```

Chain each with `addBlockedBy`. Mark `in_progress` on start, `completed` on save.

## Integration

Works with:
- `/weekly` — per-project weekly rollups feed monthly review
- `/goal-tracking` — quarterly milestone progress
- `/project` — project CLAUDE.md files provide status
- `/daily` — decision/blocker tags surfaced here
- `/push` — commit after review
