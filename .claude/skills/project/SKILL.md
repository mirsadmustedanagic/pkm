---
name: project
description: Manage career projects (netilion2, netilion-monorepo). Create/track/archive projects using the career project CLAUDE.md format with Decisions & Learnings and Weekly Progress Notes.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, TaskCreate, TaskUpdate, TaskList, TaskGet
model: sonnet
user-invocable: true
---

# Project Skill

Create, track, and archive career projects. Every project has its own `Projects/<name>/CLAUDE.md` containing status, current focus, blockers, weekly progress notes, and a decision log.

Current active projects:
- **netilion2** — primary, active
- **netilion-monorepo** — maintenance mode

## Usage

```
/project              # Interactive: create or view status
/project new          # Create a new project
/project status       # Dashboard of all active projects
/project archive <name>
```

## Commands

### `/project` or `/project new`

Creates a new project folder with a CLAUDE.md following the career project format.

**Steps:**
1. Ask for project name (kebab-case folder name).
2. Ask which yearly goal from `Goals/1. Yearly Goals (2026 - RECLAIM).md` this supports (or "none").
3. Ask role: `primary` | `secondary` | `maintenance`.
4. Create `Projects/<name>/CLAUDE.md` from the structure below.
5. If linked to a goal, add `[[Projects/<name>/CLAUDE|<name>]]` to the yearly goals file.

**Project CLAUDE.md Structure:**

```markdown
---
project: <name>
status: active
role: primary | secondary | maintenance
tags: [project, <name>]
updated: <YYYY-MM-DD>
---

# <name>

**Status:** Active — <role>
**Current phase:** [Discovery | Build | Stabilize | Maintain]
**Deep work allocation:** [Xh/week target]

---

## Current Focus

**This week's priority:**
-

**Next 3 PRs / features:**
1.
2.
3.

---

## Recently Shipped

| Date | Feature / PR | Notes |
|------|--------------|-------|

---

## Active Blockers

| Since | Blocker | Severity | Owner / Next step |
|-------|---------|----------|-------------------|

*Blockers older than 2 weeks without progress → escalate at next weekly review.*

---

## Weekly Progress Notes

*Update every Friday during weekly review.*

### Week of <YYYY-MM-DD>
- Shipped:
- In progress:
- Blockers:
- Next week priority:

---

## Decisions & Learnings

| Date | Decision / Learning | Rationale / Tradeoff | Impact |
|------|---------------------|----------------------|--------|

---

## Related
- [[2. Monthly Goals (Current)]]
- [[1. Yearly Goals (2026 - RECLAIM)]]
```

### `/project status`

Dashboard across all `Projects/*/CLAUDE.md` files.

**Steps:**
1. Glob `Projects/*/CLAUDE.md`.
2. Extract from each: name, status, role, phase, current focus, open blockers, last weekly update date.
3. Render dashboard.

**Output:**

```markdown
## Project Dashboard

| Project | Role | Phase | Current Focus | Open Blockers | Last Update |
|---------|------|-------|---------------|---------------|-------------|
| netilion2 | primary | Build | ... | 1 | 2026-07-19 |
| netilion-monorepo | maintenance | Maintain | ... | 0 | 2026-07-12 |

### Attention
- Projects with blockers >2 weeks old: [list]
- Projects with no update in 14+ days: [list]
```

### `/project archive <name>`

**Steps:**
1. Verify `Projects/<name>/` exists.
2. Confirm with user.
3. Set frontmatter `status: archived`, update phase note.
4. Move folder: `mv Projects/<name> Archives/Projects/<name>`.
5. Create `Archives/Projects/` if missing.
6. Report.

## Naming Conventions

- Folder name: kebab-case (`netilion2`, `netilion-monorepo`).
- Match the project tag: `#project/<folder-name>`.

## Cascade Integration

```
Goals/1. Yearly Goals (2026 - RECLAIM).md   <- what to achieve
        |
        v
Projects/<name>/CLAUDE.md                    <- how (this skill)
        |
        v
Daily Notes/*.md (#project/<name> tagged)    <- daily execution
```

Tasks in daily notes reference projects by tag:

```markdown
- [ ] Wire retry logic on ingest #project/netilion2
```

Decisions/learnings captured in daily notes get logged to the project's Decisions & Learnings table during Afternoon Review or Weekly Review.

## Task-Based Progress Tracking

### New Project
```
TaskCreate: subject: "Read yearly goals", activeForm: "Reading yearly goals..."
TaskCreate: subject: "Create project structure", activeForm: "Creating Projects/<name>/CLAUDE.md..."
TaskCreate: subject: "Link project to goal", activeForm: "Linking project to yearly goal..."
```

### Status Dashboard
```
TaskCreate: subject: "Scan project files", activeForm: "Scanning Projects/*/CLAUDE.md..."
TaskCreate: subject: "Compile dashboard", activeForm: "Compiling project dashboard..."
```

## Integration

Works with:
- `/daily` — surface project current focus and next PRs in Morning Setup
- `/weekly` — Friday per-project review updates project CLAUDE.md
- `/monthly` — rolls up project momentum
- `/goal-tracking` — projects link to yearly goals
- `/push` — commit project changes
