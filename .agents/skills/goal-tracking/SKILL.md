---
name: goal-tracking
description: Track progress across the career goal cascade — three-year vision, yearly goals, monthly focus, projects, weekly reviews, daily execution.
allowed-tools: Read, Grep, Glob, Edit, TaskCreate, TaskUpdate, TaskList, TaskGet
model: sonnet
---

# Goal Tracking Skill

Track and manage the career goal cascade from long-term vision to daily execution.

## Goal Hierarchy

```
Goals/0. Three Year Vision (Career).md       <- Career vision
    v
Goals/1. Yearly Goals (2026 - RECLAIM).md    <- Annual objectives
    v
Projects/*/CLAUDE.md                          <- Active projects (bridge)
    v
Goals/2. Monthly Goals (Current).md           <- Current month focus + rollups
    v
Projects/*/Weekly Reviews/*.md                <- Friday per-project reviews
    v
Daily Notes/*.md                              <- Daily execution
```

## Goal File Formats

### Three-Year Vision (Career)
Free-form vision statement scoped to career/engineering trajectory. Read for context only; not scored.

### Yearly Goals
```markdown
## 2026 Career Goals
- [ ] Goal 1 — Supported by: [[Projects/netilion2/CLAUDE|netilion2]]
- [ ] Goal 2 — Quarterly milestones: Q1 ..., Q2 ..., Q3 ..., Q4 ...
```

### Monthly Goals (Current)
```markdown
## This Month's Focus
1. **Primary project:** netilion2
2. **Deep-work target:** X hours/week
3. **Key deliverables:** ...

## Monthly Log
- Weekly rollups appended here
```

## Progress Calculation

### Checklist-Based
`Progress = (Completed checkboxes / Total checkboxes) × 100`

### Project-Contributed
For yearly goals with linked projects, aggregate:
- Recently shipped items count
- Blockers count
- Weekly progress velocity

### Time-Based Milestones
For quarterly milestones: on-track / at-risk / off-track by elapsed vs remaining time.

## Common Operations

### View Goal Progress
1. Read all Goals/ files.
2. Read all `Projects/*/CLAUDE.md`.
3. Match projects to yearly goals via wiki-link references.
4. Compute per-goal progress and flag stalled goals.

### Connect Daily Task to Cascade
Daily tasks tag by project: `#project/netilion2`, `#project/netilion-monorepo`. Project ties back to yearly goal via the project's linked goal.

### Surface Stalled Goals
- Flag yearly goals with no project activity in 14+ days.
- Flag quarterly milestones off pace.

## Project-Aware Progress

- Scan `Projects/*/CLAUDE.md`, read "Recently Shipped", "Active Blockers", "Weekly Progress Notes".
- Attribute activity to the yearly goal each project supports.
- A yearly goal with no active project → suggest `/project new`.

## Progress Report Format

```markdown
## Career Goal Progress

### Yearly Goals (2026 - RECLAIM)
| Goal | Supporting Projects | Shipped (30d) | Status |
|------|---------------------|---------------|--------|
| Goal 1 | netilion2 | 6 | On Track |
| Goal 2 | netilion-monorepo | 1 | At Risk |

### Project Status
| Project | Role | Phase | Open Blockers | Last Update |
|---------|------|-------|---------------|-------------|
| netilion2 | primary | Build | 1 | 2026-07-19 |
| netilion-monorepo | maintenance | Maintain | 0 | 2026-07-12 |

### Quarterly Milestones (Q[N])
| Milestone | Status |
|-----------|--------|

### Orphan Goals
- [Goal without active project → suggest /project new]

### Recommended Focus
1. [Stalled goal / blocker / overdue milestone]
```

## Task-Based Progress Tracking

```
TaskCreate: subject: "Read three-year vision", activeForm: "Reading Goals/0. Three Year Vision (Career).md..."
TaskCreate: subject: "Read yearly goals", activeForm: "Reading Goals/1. Yearly Goals (2026 - RECLAIM).md..."
TaskCreate: subject: "Read monthly goals", activeForm: "Reading Goals/2. Monthly Goals (Current).md..."
TaskCreate: subject: "Scan projects", activeForm: "Scanning Projects/*/CLAUDE.md..."
TaskCreate: subject: "Compute progress", activeForm: "Computing per-goal progress..."
TaskCreate: subject: "Flag stalled goals", activeForm: "Flagging goals with 14+ day inactivity..."
```

Chain dependencies so analysis waits on reads.

## Integration Points

- `/weekly` — per-project review; feed decisions/velocity back
- `/daily` — tag tasks by project so contributions attribute correctly
- `/monthly` — quarterly milestone check
- `/project` — projects are the bridge layer
