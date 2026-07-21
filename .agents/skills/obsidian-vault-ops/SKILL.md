---
name: obsidian-vault-ops
description: Read and write Obsidian vault files, manage wiki-links, process markdown with YAML frontmatter. Career-only PKM vault conventions.
allowed-tools: Read, Write, Edit, Glob, Grep
model: sonnet
---

# Obsidian Vault Operations Skill

Core operations for reading, writing, and managing files in the career-only PKM vault.

## Vault Structure

```
vault-root/
├── CLAUDE.md                                        # Root context (career-only)
├── Daily Notes/                                     # YYYY-MM-DD.md
├── Goals/
│   ├── 0. Three Year Vision (Career).md
│   ├── 1. Yearly Goals (2026 - RECLAIM).md
│   └── 2. Monthly Goals (Current).md
├── Projects/
│   ├── netilion2/CLAUDE.md
│   └── netilion-monorepo/CLAUDE.md
├── Templates/
│   ├── Daily Note - Career.md
│   └── Weekly Project Review.md
└── Archives/                                        # includes Archives/Templates/
```

## File Operations

### Reading Notes
- Read root `CLAUDE.md` first for vault conventions.
- Read the relevant `Projects/<name>/CLAUDE.md` when working on a project.
- Use Glob for structured lookups (`Daily Notes/*.md`, `Projects/*/CLAUDE.md`).

### Creating Notes
1. Check if the note already exists.
2. Use the appropriate career template (`Daily Note - Career.md` or `Weekly Project Review.md`).
3. Add YAML frontmatter with date and tags.
4. Insert wiki-links to related project / goal files.

### Editing Notes
- Preserve YAML frontmatter.
- Maintain existing wiki-links.
- Keep heading hierarchy consistent (H1 title only, H2 major sections).
- Apply the career tag scheme (below).

## Wiki-Link Format

```markdown
[[Note Name]]
[[Note Name|Display Text]]
[[Note Name#Section]]
[[Projects/netilion2/CLAUDE|netilion2]]
```

## Frontmatter

```yaml
---
date: 2026-07-21
tags: [daily-note, career]
---
```

For projects:
```yaml
---
project: netilion2
status: active
role: primary
tags: [project, netilion2]
updated: 2026-07-21
---
```

## Template Variables

- `{{date}}`, `{{date:format}}`, `{{date-1}}`, `{{date+1}}`, `{{time}}`
- `{{project}}` in `Weekly Project Review.md`

## Common Patterns

### Daily Note Creation
1. Compute today's date `YYYY-MM-DD`.
2. Check `Daily Notes/<date>.md`.
3. If missing, read `Templates/Daily Note - Career.md`.
4. Replace template variables.
5. Write to `Daily Notes/<date>.md`.

### Weekly Project Review Creation
1. For each active project, read `Templates/Weekly Project Review.md`.
2. Substitute `{{project}}` and `{{date}}`.
3. Write to `Projects/<project>/Weekly Reviews/<date>.md`.

### Decision Log Update
Add a row to the `Decisions & Learnings` table inside `Projects/<name>/CLAUDE.md`.

## Tag Scheme (Career-Only)

- **Priority:** `#priority/high`, `#priority/medium`, `#priority/low`
- **Status:** `#active`, `#waiting`, `#completed`, `#archived`
- **Project:** `#project/netilion2`, `#project/netilion-monorepo`
- **Context:** `#learning`, `#decision`, `#blocker`

The old personal contexts (`#work`, `#personal`, `#health`, `#family`) are NOT used in this vault.

## File Naming

- Daily notes: `YYYY-MM-DD.md`
- Project folders: kebab-case (`netilion2`, `netilion-monorepo`)
- Goal files: numbered with descriptor, e.g. `2. Monthly Goals (Current).md`
- Templates: Title Case with space (`Daily Note - Career.md`)

## Best Practices

1. Check root `CLAUDE.md` for conventions.
2. Preserve existing structure when editing.
3. Prefer wiki-links for internal references.
4. Always add frontmatter to new notes.
5. Log decisions/learnings in the relevant project CLAUDE.md.
