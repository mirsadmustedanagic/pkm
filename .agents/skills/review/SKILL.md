---
name: review
description: Smart review router. Detects context (time of day, Friday, end of month) and launches daily / weekly / monthly review workflows.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, TaskCreate, TaskUpdate, TaskList, TaskGet
model: sonnet
user-invocable: true
---

# Review Skill

Smart router that detects context and launches the appropriate review workflow.

## Usage

```
/review           # Auto-detect
/review daily     # Force daily (Morning Setup / Afternoon Review)
/review weekly    # Force Friday per-project weekly review
/review monthly   # Force monthly review
```

Or: "Help me review" — the right workflow starts.

## Auto-Detection Logic

### 1. Time of Day

```bash
HOUR=$(date +%H)
```

- **Before noon (< 12):** Morning Setup — delegate to `/daily` morning workflow.
- **After 3 PM (>= 15):** Afternoon Review — delegate to `/daily` afternoon workflow.
- **Midday (12–15):** Ask which routine the user wants (or default to Morning Setup if today's note is empty).

### 2. Day of Week

```bash
DAY_OF_WEEK=$(date +%u)   # 1=Mon, 5=Fri, 7=Sun
```

- **Friday (5):** Suggest weekly review — delegate to `/weekly`.
  - Overrides time-of-day if it's Friday afternoon.
  - Ask: "It's Friday — run per-project weekly review?"

### 3. Day of Month

```bash
DAY_OF_MONTH=$(date +%d)
DAYS_IN_MONTH=$(date -d "$(date +%Y-%m-01) +1 month -1 day" +%d)
```

- **Last 3 days of month:** Monthly review — delegate to `/monthly`. Overrides all others.
- **First day of month:** Suggest monthly review for the month just ended.

### 4. Staleness

- If the most recent weekly review file in `Projects/*/Weekly Reviews/` is >7 days old, suggest weekly review regardless of day.
- If no monthly review row appears in `Goals/2. Monthly Goals (Current).md` for the previous month, suggest monthly.

## Routing Behavior

1. Announce what was detected: "It's Friday afternoon — launching per-project weekly review."
2. Delegate to the target skill; that skill owns the workflow.

## Explicit Override

`/review weekly` skips detection and goes straight to the weekly workflow.

## Output on Detection

```markdown
### Review Router

**Time:** 16:20 (Afternoon)
**Day:** Friday
**Month day:** 24th

**Detected:** Weekly review (Friday override)
**Last weekly review:** 7 days ago

Launching per-project weekly review...
```

## Edge Cases

- **Monthly + Friday collide:** monthly wins.
- **No daily note exists in the morning:** create one via `/daily` first.
- **User declines suggestion:** fall through to the next detection level.
- **Explicit argument overrides everything.**

## Integration

- `/daily` — Morning Setup + Afternoon Review
- `/weekly` — Friday per-project review
- `/monthly` — Monthly rollup and planning
