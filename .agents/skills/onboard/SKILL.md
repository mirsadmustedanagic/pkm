---
name: onboard
description: Career-focused vault onboarding and context loading. First run personalizes the vault; subsequent runs load full context for the session.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
model: sonnet
user-invocable: true
---

# Onboard Skill

Interactive career-only PKM setup (first run) and context loading (subsequent runs).

## Usage

```
/onboard                    # Full onboard (setup if first run, context load otherwise)
/onboard Projects/netilion2 # Load a specific project's context
```

## First-Run Setup

If `FIRST_RUN` exists in the vault root, treat this as a fresh install.

### Step 1: Welcome
- "I'll ask a few questions to set up your career-focused PKM (~2 minutes)."
- "Answers are stored in `vault-config.json`."

### Step 2: Ask Questions (AskUserQuestion)

**Q1: Your name**
- "What should I call you?"

**Q2: Active projects**
- "Which projects are active right now? (multi-select)"
- Options: `netilion2` (default), `netilion-monorepo` (default), Add another…
- multiSelect: true

**Q3: Primary project**
- "Which is your primary project — the one you'll spend most deep-work time on?"
- Options: (populated from Q2)

**Q4: Deep-work target**
- "How many deep-work hours/week do you want to protect?"
- Options: 5, 10, 15, 20, custom

**Q5: Work style**
- "How do you prefer Claude to interact?"
- Options: Direct and concise (Recommended), Coaching and challenging, Detailed and thorough, Minimal — just do the task

There are no life-area questions. This vault is career-only.

### Step 3: Save Configuration

Write `vault-config.json`:
```json
{
  "name": "...",
  "activeProjects": ["netilion2", "netilion-monorepo"],
  "primaryProject": "netilion2",
  "deepWorkTargetHours": 15,
  "workStyle": "Direct and concise",
  "reviewDay": "Friday",
  "setupDate": "YYYY-MM-DD",
  "version": "3.1"
}
```

`reviewDay` is fixed at Friday (career weekly review cadence).

### Step 4: Do NOT edit templates or goal files
Root `CLAUDE.md`, `Goals/*.md`, and `Templates/*.md` are already career-shaped. Do not modify them during onboard.

### Step 5: Remove First-Run Marker

```bash
rm FIRST_RUN
```

### Step 6: Confirm Setup

- "Your career PKM is set up. Active projects: [list]. Primary: [name]."
- "Try `/daily` to run Morning Setup."
- "`/review` auto-detects daily/weekly/monthly."

Then proceed to standard context loading.

## Standard Context Loading (Subsequent Runs)

### What This Skill Does

1. **Read root `CLAUDE.md`** — vault system context.
2. **Read active project CLAUDE.md files** — `Projects/netilion2/CLAUDE.md`, `Projects/netilion-monorepo/CLAUDE.md` (and any others from `vault-config.json`).
3. **Read current goals context:**
   - `Goals/2. Monthly Goals (Current).md`
   - `Goals/1. Yearly Goals (2026 - RECLAIM).md` (skim for quarterly milestones)
4. **Load recent state:**
   - Last 7 daily notes from `Daily Notes/`
   - Latest weekly review from `Projects/*/Weekly Reviews/`
5. **Read `vault-config.json`** — apply name, primary project, deep-work target, work style.

## Context Hierarchy

```
vault/
├── CLAUDE.md                                  [1] Global context
├── Goals/2. Monthly Goals (Current).md        [2] Month focus
├── Projects/netilion2/CLAUDE.md               [3] Primary project
├── Projects/netilion-monorepo/CLAUDE.md       [4] Secondary
└── Daily Notes/                               [5] Recent state
```

## Selective Loading

```
/onboard Projects/netilion2      # Only netilion2 project
/onboard Goals                   # Only goal cascade
```

## Session Summary Output

After context load, print a compact summary:

```markdown
### Session Context Loaded
- **Primary project:** netilion2 — [current focus line]
- **Monthly focus:** [from Goals/2. Monthly Goals (Current).md]
- **Open blockers:** N (netilion2: N, monorepo: N)
- **Last weekly review:** [date]
```

## Privacy

Do not include credentials, tokens, or internal customer data in `CLAUDE.md` or `vault-config.json`. Use `CLAUDE.local.md` (git-ignored) for anything private.

## Integration

Works with:
- All other skills (provides context)
- `/daily` — Morning Setup uses loaded project focus
- `/weekly` — informed per-project review
- `/monthly` — full-context monthly review
- `/project` — project overview
