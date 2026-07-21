---
name: adopt
description: Scaffold the career-only PKM system onto an existing Obsidian vault. Scans structure, maps folders, generates configuration — preserves your existing files.
allowed-tools: Read, Write, Edit, Glob, Grep, Bash, AskUserQuestion
model: sonnet
user-invocable: true
---

# Adopt Skill

Bring Your Own Vault (BYOV) — install the career-only Claude PKM system onto an existing Obsidian vault.

## Usage

```
/adopt    # Run from the root of your existing Obsidian vault
```

## When to Use

- Existing Obsidian vault, and you want the career PKM overlay added.
- Don't want to start from the vault template.
- Want to keep your current folder structure.

This skill is career-focused. It sets up structure for engineering projects, weekly per-project reviews, and a decision log. It does NOT scaffold life-area folders (health, relationships, finance, creativity).

## Phase 1: Scan Vault Structure

1. List top-level directories (excluding `.obsidian`, `.git`, `.claude`, `.trash`, `.claude-plugin`).
2. For each directory, gather signals:
   - Count `.md` files.
   - Detect date-named files (`YYYY-MM-DD*.md`) → daily notes.
   - Grep for goal/review/template keywords.
   - Look for `CLAUDE.md` inside subdirs → projects.
3. Present findings.

## Phase 2: Map Folders to Roles

Roles to map:

| Role | Purpose | Detection Signal |
|------|---------|-----------------|
| Daily Notes | Daily journal | Date-named files |
| Goals | Career goal cascade | Goal-keyword files |
| Projects | Engineering projects (each with CLAUDE.md) | Subdirs with CLAUDE.md |
| Templates | Reusable structures | Files in Templates/ |
| Archives | Completed/inactive | Folder named Archive(s) |

Use AskUserQuestion to confirm each mapping. Offer to create the folder if none exists. There is no Inbox role in the career-only variant (kept optional if user already has one).

**Edge cases:**
- Existing root `CLAUDE.md`: back up as `CLAUDE.md.backup` before merging.
- Multiple candidates: ask user.

## Phase 3: Personalize Preferences

Ask (AskUserQuestion):

**Q1: Your name**

**Q2: Active projects**
- "Which projects are active? Enter folder names under Projects/."
- Default suggestion for engineering vaults: any subdirs with a `CLAUDE.md`.

**Q3: Primary project**
- From the list in Q2.

**Q4: Deep-work target (hours/week)**

**Q5: Work style**
- Direct and concise (Recommended), Coaching, Detailed, Minimal.

Review cadence is fixed: Friday per-project weekly review.

## Phase 4: Generate Configuration

### 4a. `.claude/settings.json`

Scope permissions to the user's mapped folders:

```json
{
  "permissions": {
    "allow": [
      "Read",
      "Write **/{mapped-daily}/**",
      "Write **/{mapped-goals}/**",
      "Write **/{mapped-projects}/**",
      "Write **/{mapped-templates}/**",
      "Edit **/{mapped-daily}/**",
      "Edit **/{mapped-goals}/**",
      "Edit **/{mapped-projects}/**",
      "Glob",
      "Grep"
    ]
  }
}
```

### 4b. Root `CLAUDE.md`

Generate a root `CLAUDE.md` describing the vault as career-only. Use the standard career template but substitute mapped folder names. If an existing `CLAUDE.md` was present, merge in user-specific mission/notes sections.

### 4c. `vault-config.json`

```json
{
  "name": "...",
  "activeProjects": ["..."],
  "primaryProject": "...",
  "deepWorkTargetHours": 15,
  "workStyle": "Direct and concise",
  "reviewDay": "Friday",
  "setupDate": "YYYY-MM-DD",
  "version": "3.1",
  "adoptedVault": true,
  "folderMapping": {
    "dailyNotes": "Daily Notes",
    "goals": "Goals",
    "projects": "Projects",
    "templates": "Templates",
    "archives": "Archives"
  }
}
```

### 4d. Env vars

Write `.claude/hooks/adopt-env.sh` exporting `DAILY_NOTES_DIR`, `GOALS_DIR`, `PROJECTS_DIR`, `TEMPLATES_DIR`, `ARCHIVES_DIR`. Ensure `session-init.sh` sources it.

## Phase 5: Scaffold Missing Pieces

Ask before creating.

### 5a. Career Goal Cascade
If the mapped goals folder is empty, offer to create:
- `0. Three Year Vision (Career).md`
- `1. Yearly Goals (<YYYY>).md`
- `2. Monthly Goals (Current).md`

### 5b. Career Templates
If templates folder is empty, offer to add:
- `Daily Note - Career.md`
- `Weekly Project Review.md`

(Older multi-purpose templates are not scaffolded.)

### 5c. Project CLAUDE.md
For each declared active project without a CLAUDE.md, offer to scaffold the career project structure (status, current focus, blockers, weekly progress notes, decisions & learnings).

### 5d. Claude Config Dirs
Ensure `.claude/skills/`, `.claude/rules/`, `.claude/hooks/`, `.claude/agents/` exist.

## Phase 6: Verify & Next Steps

Validate:
- `vault-config.json` is valid JSON.
- Mapped folders exist.
- Root `CLAUDE.md` present.
- `adopt-env.sh` present and executable.

Summary:

```
Adoption complete!
Vault: /path/to/vault
Active projects: netilion2, netilion-monorepo
Primary: netilion2
Mapped folders:
  Daily Notes → Daily Notes/
  Goals       → Goals/
  Projects    → Projects/
  Templates   → Templates/
  Archives    → Archives/
```

Next steps:
- "Try `/daily` for Morning Setup."
- "Try `/review` — auto-detects daily/weekly/monthly."
- "`/push` to commit adoption changes."

## Error Handling

- No `.obsidian` dir → warn "Not an Obsidian vault. Continue anyway?"
- Already adopted (`adoptedVault: true`) → ask before regenerating.
- Permission errors on `.claude/` → surface path and instructions.

## Integration

Works with:
- `/onboard` — adopt replaces onboard for existing vaults
- `/daily`, `/weekly`, `/monthly`, `/project`, `/push` — all respect mapped folders
