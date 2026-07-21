---
date: 2026-07-21
status: review-required
tags: [audit, skills, career-focus]
---

# Skills & Agents Audit: Career-Focus Update

**Review Date:** 2026-07-21  
**Status:** ⚠️ Needs Updates — Agents were designed for multi-area life PKM, now shifting to career-only

---

## 📋 Summary

| Component | Status | Action |
|-----------|--------|--------|
| **goal-aligner** | ⚠️ Partially Broken | Needs career-focus rewrite |
| **weekly-reviewer** | ⚠️ Partially Broken | Needs project-centric rewrite |
| **inbox-processor** | ⚠️ Partially Broken | Career inbox only; remove personal routing |
| **note-organizer** | ✅ Still Valid | Works for career vault structure |
| **Rules (4 files)** | ⚠️ Outdated | Need career-focus adaptation |
| **Skills (in CLI)** | ⚠️ Not in repo | Global skills exist but need career variants |

---

## 🔍 Detailed Audit

### 1. **goal-aligner Agent** — ⚠️ Needs Update

**Current Purpose:** "Analyze alignment between daily activities and long-term goals"

**Problem:**
- Scans `3-Year Vision`, `Annual Objectives`, `Monthly Priorities` — ✅ Still valid
- Looks for **multi-area time investment** (health, relationships, personal, career) — ❌ NO LONGER NEEDED
- Calculates % of time in each life area — ❌ REMOVED (career-only now)
- Looks for balance across all areas — ❌ NOT APPLICABLE

**What Should Change:**
- Scan only **Career goals** (3-year → yearly → quarterly → monthly)
- Analyze: "Is daily work aligned with netilion2/monorepo focus?"
- Calculate: "% of work time on meaningful vs. reactive tasks"
- Output: "Career alignment score" (not life-balance score)

**New Purpose:**
> "Analyze alignment between daily work and career/project goals. Identify if deep work time is protected, if blockers are resolved, if learnings are captured."

**Effort to Fix:** Medium (30 min) — Logic stays similar, just filter to career domain

---

### 2. **weekly-reviewer Agent** — ⚠️ Needs Major Update

**Current Purpose:** "Facilitate comprehensive weekly review process. Analyze past week's daily notes, calculate goal progress, and help plan next week."

**Problem:**
- Reads 3-year, annual, monthly goals — ✅ Still valid
- Outputs "goal progress for each goal" across **all life areas** — ❌ OUTDATED
- Calculates goal completion % globally — ❌ NOT APPLICABLE (career-only)
- Includes life-balance coaching ("What worked in relationships?") — ❌ REMOVED

**What Should Change:**
- Focus ONLY on **career goals + project progress**
- Add project-specific metrics: PRs merged, features shipped, blockers resolved
- Calculate **velocity trends** (PRs/week this week vs. last week vs. monthly avg)
- Output: Project snapshots, decision/learning log, next week focus
- Remove: Balance, personal reflection, life-area split

**New Purpose:**
> "Facilitate weekly project review. Scan past week's daily notes, update project CLAUDE.md files with progress, calculate velocity, identify blockers, plan next week focus."

**Effort to Fix:** High (1-2 hours) — Significant logic change from life-balance to project-centric

---

### 3. **inbox-processor Agent** — ⚠️ Needs Minor Update

**Current Purpose:** "Process inbox items using GTD principles"

**Problem:**
- Categorizes items into: **#next-action, #project, #waiting, #someday, #reference** — ✅ Good
- Routes to "today's daily note or appropriate project" — ✅ Good
- Mentions "Context tags: #work, #personal, #health, #learning, #family" — ❌ REMOVE non-work tags
- Assumes mixed personal/work inbox — ❌ NOW CAREER-ONLY

**What Should Change:**
- Remove personal context tags (#personal, #family, #health)
- Assume all inbox items are **work-related**
- Route to: daily note, project CLAUDE.md, or team channels
- Add: Link captured decisions/learnings to project logs

**New Purpose:**
> "Process work inbox using GTD principles. Categorize items into next-actions, projects, blockers, or learnings; route to appropriate projects or daily notes."

**Effort to Fix:** Low (20 min) — Just remove personal routing, keep GTD logic

---

### 4. **note-organizer Agent** — ✅ Still Valid

**Current Purpose:** "Organize and restructure vault notes. Fix broken links, consolidate duplicates, suggest connections."

**Status:** ✅ This agent still works!

**Why:**
- Scans vault structure — ✅ Works for career vault
- Fixes broken links — ✅ Works for career-only structure
- Consolidates tags — ✅ Works (just fewer tags now)
- Archives stale notes — ✅ Works (archives old daily notes, projects)
- Suggests connections — ✅ Works (links between projects, goals, decisions)

**Minor Adjustment:**
- Remove examples referencing personal areas in documentation
- Add: Maintaining decision log in project files

**Effort to Fix:** Minimal (10 min) — Just update examples and documentation

---

### 5. **Rules** — ⚠️ Outdated

#### **markdown-standards.md** — ⚠️ Needs Career Focus
**Current:** Examples include personal areas, multi-context tags
**Update needed:**
- Remove tags: #context/personal, #context/health, #context/family, #context/learning
- Keep tags: #context/work (or remove category entirely, assume all work)
- Update examples to use netilion2, monorepo, engineering context
- Add: Decision/learning log format for project files

**Effort:** Low (15 min)

#### **productivity-workflow.md** — ⚠️ Needs Major Update
**Current:** Covers daily/weekly/monthly rituals across all life areas
**Update needed:**
- Remove: Energy levels, life-area tracking, personal goal cascade
- Keep: SMART goals, daily planning, weekly review structure
- Add: Project velocity tracking, blocker escalation, decision capture
- Add: Deep work protection (deep work block on calendar)
- Rewrite example to show career-only cascade (3-yr vision → yearly → quarterly → monthly → weekly → daily)

**Effort:** High (1 hour)

#### **project-management.md** — ✅ Still Mostly Valid
**Current:** Structures project folders, tracks status
**Status:** Pretty good! Just needs:
- Update examples to netilion2/monorepo
- Add: "Decisions & Learnings" section requirement
- Add: Weekly update cadence (Friday project reviews)

**Effort:** Low (20 min)

#### **task-tracking.md** — ✅ Still Valid
**Current:** Explains session tasks vs. markdown checkboxes
**Status:** Perfect, no changes needed

**Effort:** None

---

## 📊 Audit Summary Table

| Component | Current State | Career-Focus Ready? | Effort to Fix | Priority |
|-----------|---------------|-------------------|---------------|----------|
| goal-aligner | Multi-area | ❌ No | 30 min | Medium |
| weekly-reviewer | Multi-area | ❌ No | 1-2 hours | HIGH |
| inbox-processor | Mixed work/personal | ⚠️ Partial | 20 min | Low |
| note-organizer | Generic | ✅ Yes | 10 min | Minimal |
| markdown-standards.md | Multi-area | ⚠️ Partial | 15 min | Low |
| productivity-workflow.md | Multi-area | ⚠️ Partial | 1 hour | HIGH |
| project-management.md | Generic | ✅ Yes | 20 min | Low |
| task-tracking.md | Generic | ✅ Yes | None | ✅ Done |

---

## 🚨 What Breaks First

When you use your career-only PKM with old agents/rules:

1. **`/weekly` skill calls weekly-reviewer** 
   - Tries to read multi-area goals (now removed)
   - Outputs life-area metrics (not applicable)
   - **Result:** Confusing output, missing project metrics

2. **`/review` (smart router) detects `sunday` → calls weekly-reviewer**
   - Same issue as above

3. **Rules don't reflect your actual structure**
   - Projects don't know about decision logs
   - Markdown standards include removed tags
   - Productivity workflow talks about personal time allocation

---

## ✅ What Still Works

- ✅ `/daily` — Creates daily note (template just needs content simplification)
- ✅ `/push` — Commits to git (works regardless)
- ✅ `/onboard` — Sets up vault (works but talks about multi-area)
- ✅ `note-organizer` agent — Works for any vault structure
- ✅ `task-tracking.md` — Rules still apply
- ✅ `project-management.md` — Almost perfect (just needs examples update)

---

## 🎯 Recommended Fix Sequence

### Phase 1: Update Rules (1.5 hours)
1. **markdown-standards.md** (15 min) — Remove personal tags, add decision log format
2. **productivity-workflow.md** (60 min) — Career-only cascade, deep work protection, blocker escalation
3. **project-management.md** (20 min) — Add decision logs, update examples

### Phase 2: Update Agents (3 hours)
1. **inbox-processor** (20 min) — Remove personal routing
2. **note-organizer** (10 min) — Update docs and examples
3. **goal-aligner** (30 min) — Rewrite for career-only alignment
4. **weekly-reviewer** (1-2 hours) — Major rewrite for project-centric review

### Phase 3: Test & Refine (30 min)
1. Run `/weekly` skill — Should work with updated weekly-reviewer
2. Check for broken links from removed goals
3. Verify daily note template still works

---

## 📝 Implementation Notes

### For Rules Updates
- Keep the structure (YAML frontmatter + markdown content)
- Update descriptions in frontmatter
- Replace examples throughout
- Add new sections for: blocker escalation, decision capture, deep work protection

### For Agent Updates
- Update frontmatter: `description` field
- Update section headers and explanations
- Remove multi-area references
- Add project/blocker tracking references
- Keep output format (mostly works, just focus on career metrics)

### For Skills Testing
After updates, test:
```
/daily                    → Creates work-focused daily note
/weekly                   → Shows project metrics, velocity, blockers
/review                   → Detects context, calls appropriate ritual
/push                     → Commits changes (should still work)
```

---

## ⚠️ Risks & Mitigations

**Risk:** Old rules still reference deleted goal areas  
**Mitigation:** Update all rules before using new system  

**Risk:** Agents output confusing multi-area metrics  
**Mitigation:** Rewrite agent descriptions and output templates  

**Risk:** Inbox processor routes items to removed personal areas  
**Mitigation:** Remove personal routing, test GTD flow  

**Risk:** Daily notes still try to capture personal data  
**Mitigation:** Update daily template FIRST, test template

---

## 🔧 Next Steps

**Choose one:**

1. **Option A:** Start with Rules-only fix (~1.5 hours)
   - Update rules now
   - Agents will mostly work
   - Fine-tune agents in Phase 2

2. **Option B:** Full overhaul (3-4 hours)
   - Update rules + agents together
   - Comprehensive test after
   - Ready to use immediately

3. **Option C:** Gradual rollout (5-6 hours spread over week)
   - Day 1: Rules update
   - Day 2: inbox-processor + note-organizer
   - Day 3: goal-aligner
   - Day 4: weekly-reviewer (big one)
   - Day 5: Test all together

**Recommendation:** Go with **Option B** (full overhaul) — you have the new templates ready, time to align agents/rules to match.

---

**Status:** Ready to proceed once you choose approach.

*Created: 2026-07-21*  
*Audit Type: Career-Focus Update*  
*Severity: Medium (agents need updates to work well)*
