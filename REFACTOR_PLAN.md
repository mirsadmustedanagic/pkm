---
date: 2026-07-21
status: active
---

# PKM Refactoring Plan: Career-Focused Engineering System

## Problem Statement

You inherited a template-based PKM system designed for multi-area life management (career, health, relationships, finance, creativity). However, your actual need is **simpler and more focused**: a career/business PKM that helps you:

1. **Know what to work on each day** — Clear prioritization between netilion2 features and monorepo maintenance
2. **See long-term project progress** — Track development velocity, feature completion, blockers across weeks
3. **Protect deep work time** — Visualize when you're context-switching and actively guard against interruptions
4. **Systematize learnings** — Capture decisions, architectural insights, lessons from completed work

The current system has:
- ✅ Good structure (goal cascade, templates, rules)
- ❌ Too much "personal life" scaffolding (health goals, relationships, finance, creativity sections)
- ❌ No project tracking designed for engineering work (sprints, PRs, blockers)
- ❌ No daily/afternoon review ritual (you want daily morning + afternoon cadence)
- ❌ Templates don't reflect your actual work (netilion2, netilion-monorepo)

**Outcome:** Personalize this into a **career-focused engineering PKM** that reflects your real work and supports your review cadence.

---

## Solution

Create a **lean, purpose-built system** organized around:

1. **Goals Cascade (Career-only)**
   - Remove all personal life areas (health, relationships, finance, creativity)
   - Keep: 3-year vision → yearly → quarterly → monthly → weekly focused on meaningful work and professional growth
   - Align with your 2026 "RECLAIM" theme

2. **Project Hub**
   - One CLAUDE.md per active project (netilion2, netilion-monorepo)
   - Track: status, current focus, next actions, blockers, learnings
   - Each project gets weekly review for progress visibility

3. **Daily System (Morning + Afternoon)**
   - **Morning (5 min):** Set ONE Big Thing for today, identify which project(s), block deep work time
   - **Afternoon (5 min):** Capture what you shipped, what you learned, what blocked you, what's next
   - Use daily notes as decision/learning journal, not a life log

4. **Weekly Review (Friday)**
   - Review progress on each project (netilion2 feature completion, monorepo status)
   - Calculate velocity, identify patterns in blockers
   - Plan next week's focus and adjust priorities

5. **Decision Log**
   - New section in project files to capture architecture decisions, tradeoffs, learnings
   - Becomes your technical knowledge base over time

---

## Implementation Plan: Tiny Commits

Each step leaves your vault in a working state. You can stop at any point.

### Phase 1: Strip Personal Content (5 commits)

**Commit 1.1: Remove unused life-area goals**
- Delete personal goal sections from:
  - `Goals/0. Three Year Goals.md` — Remove Finance, Creativity & Hobbies sections
  - `Goals/1. Yearly Goals.md` — Remove Finance, Creativity, Relationships sections, keep Career + Health (stress management only)
  - `Goals/2. Monthly Goals.md` — Remove all non-career must-dos
- Keep: Career-focused goals only
- **Testing:** Verify goal documents still render and cascade makes sense

**Commit 1.2: Rename goal files to reflect career focus**
- Rename `0. Three Year Goals.md` → `0. Three Year Vision (Career).md`
- Rename `1. Yearly Goals.md` → `1. Yearly Goals (2026 - RECLAIM).md`
- Rename `2. Monthly Goals.md` → `2. Monthly Goals (Current).md`
- Update all links (backlinks will auto-fix in Obsidian)
- **Testing:** All internal links work

**Commit 1.3: Replace personal daily template with career-focused version**
- Create new `Templates/Daily Note - Career.md`
- Remove sections: Personal tasks, Health/Wellness, Gratitude, Energy levels, Screen time
- Keep/refactor: Today's Focus, Time Blocks (work-only), Must-Do tasks, Meeting notes
- Add new sections: Project focus (which project today?), Decisions/Learnings, Blockers, Next actions
- **Testing:** Template renders and is useful for a work day

**Commit 1.4: Delete example personal content**
- Remove `Projects/Example Project/` (Spanish learning — not relevant)
- Clean `Daily Notes/` — remove `2024-01-15-EXAMPLE.md`
- **Testing:** Vault structure clean and focused

**Commit 1.5: Update CLAUDE.md for career focus**
- Rewrite introduction to reflect career-only PKM
- Update Available Skills section (remove `/monthly`, `/weekly` generic; add project-tracking focus)
- Update examples to use netilion2 instead of Spanish learning
- Update best practices to address your pain points (daily prioritization, project tracking, learning capture)
- **Testing:** README reflects new system purpose

### Phase 2: Build Project Tracking (3 commits)

**Commit 2.1: Create project CLAUDE.md for netilion2**
- Create `Projects/netilion2/CLAUDE.md` with:
  - Project status, current phase
  - Recent completed features (with dates)
  - Current focus / next 3 PRs
  - Active blockers with severity
  - Weekly progress notes (updated each Friday)
  - Decision log (key architectural choices, tradeoffs)
- **Testing:** File renders, provides clear snapshot of project status

**Commit 2.2: Create project CLAUDE.md for netilion-monorepo**
- Create `Projects/netilion-monorepo/CLAUDE.md` with:
  - Status: Maintenance mode
  - Recent fixes/maintenance (last 4 weeks)
  - Known issues/tech debt
  - Maintenance cadence (how often you touch it?)
  - When to escalate vs. quick fix
- **Testing:** File clearly indicates maintenance-mode status

**Commit 2.3: Create weekly project review template**
- Create `Templates/Weekly Project Review.md`
- Structure: Project name, week of, completed this week, in-progress, blockers, velocity notes, next week priorities
- This gets copied once/week for each project at Friday review
- **Testing:** Template is simple enough to fill in 10 min/project

### Phase 3: Reshape Goals (3 commits)

**Commit 3.1: Rewrite Three-Year Vision (career)**
- Focus on: meaningful work clarity, engineering depth, impact on team/projects
- Remove: personal growth, relationships, health as separate goals (these are *not* your focus per your request)
- Success metrics: career clarity, project leadership, technical depth
- Link to 2026 yearly goals
- **Testing:** Vision is inspiring and career-specific

**Commit 3.2: Rewrite Yearly Goals (2026 RECLAIM)**
- Restructure around: Project mastery, decision-making clarity, knowledge capture, protected deep work
- Q3: Establish daily/weekly review ritual, clarify project direction
- Q4: Build momentum on netilion2, systematize learnings
- Q1 2027: Assess impact and technical growth
- **Testing:** Goals align with your pain points (prioritization, project tracking, learning capture)

**Commit 3.3: Create current monthly goals (July 2026)**
- Focus: Establish morning + afternoon review habit, get netilion2 project CLAUDE.md up to date, complete one learning capture per week
- Concrete: Run daily review 4 weeks, capture 4 architectural decisions in project logs
- Success: Feel confident about daily priorities and see project progress on weekly review
- **Testing:** Monthly goals are achievable and feed your daily system

### Phase 4: Implement Daily System (2 commits)

**Commit 4.1: Create July daily notes (first week)**
- Use new career-focused template
- Fill in: Morning focus, project selection, blockers, learnings each day
- Link to project CLAUDE.md files for context
- **Testing:** Daily notes are lightweight, capture what matters, connect to projects

**Commit 4.2: Set up daily review ritual capture**
- Create lightweight "Afternoon Review" checklist:
  - [ ] What did I ship today?
  - [ ] What blocked me?
  - [ ] One learning or decision to log in project file?
  - [ ] Next highest priority for tomorrow?
- Add to daily template as optional end-of-day section
- **Testing:** Afternoon review takes < 5 minutes, surfaces blockers for weekly review

### Phase 5: Knowledge Capture (1 commit)

**Commit 5.1: Add decision/learning log to project files**
- Add `## Decisions & Learnings` section to each project CLAUDE.md
- Format: Date | Decision/Learning | Impact | Related decisions
- Monthly consolidation: move old entries to project archive
- **Testing:** Section is easy to append to during afternoon reviews

### Phase 6: Clean Up & Documentation (2 commits)

**Commit 6.1: Update rules for career focus**
- Edit `.claude/rules/markdown-standards.md` — remove personal content examples
- Edit `.claude/rules/productivity-workflow.md` — refocus on project velocity, deep work protection
- Edit `.claude/rules/task-tracking.md` — add guidance on project-level task tracking
- Update project-management.md with netilion2/monorepo specific guidance
- **Testing:** Rules reflect career-focused workflow

**Commit 6.2: Archive template files**
- Move unused templates to `Archives/Templates/`:
  - Weekly Review Template → Archive (replace with Project Review Template)
  - Project Template → Archive (replace with career-specific template)
- Keep: Daily Note - Career, Weekly Project Review, new Project CLAUDE.md template
- **Testing:** Templates folder is clean and reflects active system

---

## Decision Document

### Modules & Interfaces to Change

**Goals Cascade** — Removing 4 life area branches (personal growth, health, relationships, finance), keeping career-only
- Input: Your 3-year vision for work
- Output: Annual → quarterly → monthly → weekly goals
- Change: Single goal thread instead of multi-area matrix

**Project Tracking** — New lightweight project system for netilion2 + monorepo
- Per-project file with status, focus, blockers, decisions
- Weekly update snapshot for velocity/progress
- Input: Your work week
- Output: Clear project status, decision log

**Daily System** — Morning + afternoon cadence replacing generic daily template
- Morning: 5 min, set focus and project for day
- Afternoon: 5 min, capture ship, blockers, learnings
- Input: Your daily work
- Output: Decision journal, blocker visibility, learning systematization

**Review Cycle** — Friday project reviews instead of multi-area weekly review
- Input: Week of work on projects
- Output: Progress snapshot, velocity calculation, next week priorities
- Change: Project-centric instead of life-area centric

### Technical Clarifications

1. **Project vs. Goal relationship:** Projects (netilion2, monorepo) support yearly goals (meaningful work clarity, deep work capacity). Goals *drive* project selection, projects *feed back* learnings into next cycle.

2. **Daily note storage:** Keep in `Daily Notes/YYYY-MM-DD.md` format, but content is work-only (no personal captures).

3. **Blockers visibility:** Captured daily in afternoon review, surfaced in project CLAUDE.md, reviewed weekly. Blockers older than 2 weeks without progress trigger escalation questions.

4. **Learning capture:** Architectural decisions, tradeoffs, patterns learned go into project decision log. Monthly, consolidate into lessons for yearly review input.

5. **Time blocks:** Morning planning includes explicit "deep work block" time — this is protected, not for meetings. Conflicts with deep work block trigger daily note callout.

### Architectural Decisions

1. **Single-project focus per day:** Morning note includes "Primary project for today" to combat context-switching pain
2. **Lightweight weekly review:** 15 min/project, snapshot-based not reflective. Full reflection happens quarterly.
3. **Decision log first:** Before capturing learnings generally, capture decisions. Decisions have immediate consequences; learnings are extracted from decisions over time.
4. **No life metrics:** Energy levels, health, personal satisfaction removed from daily tracking. System is work-only.

---

## Testing Decisions

### What Makes a Good Test

For a PKM system, "testing" means:
- **Daily notes render** and provide useful capture space without friction
- **Project CLAUDE.md files stay current** through weekly reviews (validation: Friday review takes < 20 min to update both projects)
- **Blockers surface** (validation: a blocker from Monday is visible by Friday review without needing to re-read all daily notes)
- **Learnings are actually captured** (validation: at month-end you can point to 4-8 decisions/learnings logged in project files)
- **Daily prioritization works** (validation: you can answer "what's my ONE focus today" within 2 min each morning)

### What to Test During Implementation

**During Phase 1:** Vault structure is clean, no broken links
**During Phase 2:** Project files render and update cleanly through one full week
**During Phase 3:** Goals feel motivating and specific to your work
**During Phase 4:** Daily notes capture what matters; morning setup takes < 5 min, afternoon review < 5 min
**During Phase 5:** Decisions are easy to append to project files

### Prior Art

- **Blocker surfacing:** Similar to sprint review standups (blockers raised, discussed, moved or resolved)
- **Decision log:** Similar to RFC/decision record format (date, context, decision, consequences, alternatives considered)
- **Project snapshots:** Similar to weekly status update emails (what shipped, what's next, what's stuck)
- **Daily focus note:** Similar to daily standup talking points (what I did, what blocked me, what I'll do next)

---

## Out of Scope

- Personal life management (health goals, relationships, financial planning, creativity pursuit)
- Team/collaboration tools (this is for your individual clarity, not team coordination)
- Automation/scripting (daily notes, project reviews are manual captures)
- Multi-project sprint planning (this is for your prioritization, not formal sprint management)
- Metrics/analytics dashboards (velocity charts, burndown, etc. — keep it simple)
- Integrations with external tools (Jira, GitHub, Slack, etc.)

---

## Further Notes

### Why This Works for Your Pain Points

1. **"Don't know what to work on each day"** → Morning daily note forces ONE focus + project selection before checking messages
2. **"Lose track of long-term projects"** → Weekly project review snapshots show momentum; you see progress and completion
3. **"Too much context-switching"** → Daily note includes deep work block time; afternoon review surfaces conflicts
4. **"Don't capture learnings"** → Decision log in project files makes capture lightweight; reviewed during project updates

### Timeline

- **Phase 1 (Strip):** 30 min, 5 commits
- **Phase 2 (Projects):** 45 min, 3 commits
- **Phase 3 (Goals):** 60 min, 3 commits
- **Phase 4 (Daily):** 20 min, 2 commits (one-time setup, then ongoing use)
- **Phase 5 (Knowledge):** 10 min, 1 commit
- **Phase 6 (Cleanup):** 20 min, 2 commits

**Total:** ~3 hours hands-on work, spread over 1-2 weeks as you live with it

### Success Criteria (4-Week Test)

By August 18, 2026:
- [ ] Morning planning takes < 5 min; you consistently identify ONE focus
- [ ] Afternoon reviews happen 4+ days/week and surface real blockers
- [ ] Weekly Friday project reviews show clear progress metrics (PRs completed, features shipped, blockers resolved)
- [ ] At least 8 decisions/learnings captured in project files
- [ ] No broken links; vault structure is clean

If these are true, the refactor is successful. If not, adjust by retro-fitting learnings back into the system design.

---

**Next Step:** Pick a phase to start with. I recommend starting with **Phase 1 (Strip Personal Content)** to simplify the vault structure, then **Phase 2 (Build Projects)** to get your real work visible.

*Created: 2026-07-21*  
*Ready to execute: Yes*
