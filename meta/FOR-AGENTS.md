# Protocol for AI Agents

**Purpose**: This document defines how you should operate when working on features using this system.

**When to read this**: Human will point you here with: "Use meta-v2 system" or "Read meta-v2/FOR-AGENTS.md"

---

## Core Principles

1. **SSOT First**: Always read `00-FEATURE-OVERVIEW.md` before anything else
2. **Append, Don't Recreate**: Add to `03-PROGRESS-LOG.md`, never create new summaries
3. **Respect Limits**: Documents have max lengths - enforce them
4. **Be Specific**: File paths, line numbers, exact next tasks
5. **Confirm Major Changes**: Ask before refactoring, big changes

---

## The 5 Core Documents

Located in `/claude/` (project root):

```
00-FEATURE-OVERVIEW.md     ← SSOT - read this FIRST every session
01-REQUIREMENTS.md         ← What to build (max 3 pages)
02-IMPLEMENTATION-PLAN.md  ← How to build (max 4 pages, phase-based)
03-PROGRESS-LOG.md         ← Session log (append-only, unlimited)
04-TESTING-CHECKLIST.md    ← Test scenarios (max 2 pages)
```

**Never create other status/summary documents**. If info doesn't fit in these 5, it goes in `03-PROGRESS-LOG.md`.

---

## Meta-Instruction Handlers

When human uses meta-instructions (shortcuts starting with `/`), follow these protocols:

### `/start <feature-name>`

**Intent**: Initialize new feature

**Protocol**:
1. Create `00-FEATURE-OVERVIEW.md` from template
   - Set feature name
   - Set status: "Planning"
   - Set started date
2. Create `01-REQUIREMENTS.md` from template
   - Add obvious requirements from human's description
   - Add 3-5 clarifying questions
3. Present questions to human
4. Wait for answers (don't proceed to implementation yet)

**Response template**:
```
I'll create the foundation for [feature-name].

Created:
- claude/00-FEATURE-OVERVIEW.md (draft)
- claude/01-REQUIREMENTS.md (draft)

Questions about requirements:
1. [Question 1]
2. [Question 2]
3. [Question 3]

Please answer these so I can create an implementation plan.
```

**Next steps**: After human answers → Create `02-IMPLEMENTATION-PLAN.md` → Wait for approval

---

### `/continue`

**Intent**: Resume work on existing feature

**Protocol**:
1. Read `00-FEATURE-OVERVIEW.md` (SSOT)
   - Extract: feature name, current status, current phase
2. Read last entry in `03-PROGRESS-LOG.md`
   - Extract: last completed item, next task
3. Summarize understanding (max 4 sentences)
4. State specific next task
5. Ask for confirmation

**Response template**:
```
Feature: [Name from SSOT]
Status: [Status from SSOT]
Current Phase: [Phase X - Name]

Last completed: [From progress log]
Next task: [Specific task with file path]

Ready to proceed with [next task]?
```

**Do NOT**:
- Create new summary documents
- Re-read entire codebase (focus on specific files)
- Start work without confirmation
- Assume context from previous session (always re-read SSOT)

---

### `/wrap`

**Intent**: End session with proper handoff

**Protocol**:
1. Update `02-IMPLEMENTATION-PLAN.md`:
   - Mark any completed phases with `[x]`
2. Append to `03-PROGRESS-LOG.md`:
   ```markdown
   ## [YYYY-MM-DD] Session N

   **Duration**: [X hours/minutes]
   **Phase**: [Current phase]

   **Completed**:
   - [x] Item 1
   - [x] Item 2

   **Issues Encountered & Resolved**:
   - Issue: [desc] → Solution: [desc] → Location: file.ts:line

   **Next Session Start Here**:
   Priority 1: [Most important next task]
   Priority 2: [Second task]

   Context: [Any specific knowledge needed]
   Files: [Files to review]

   Quick start: "/continue"
   ```
3. Update `00-FEATURE-OVERVIEW.md` if major milestone reached
4. Summarize session to human

**Response template**:
```
Session summary:
✓ Completed: [List]
✓ Tests: [Status]

Updated:
- 03-PROGRESS-LOG.md (with handoff)
- 02-IMPLEMENTATION-PLAN.md (marked Phase X complete)

Next session: [Specific next task]
```

---

### `/status`

**Intent**: Quick status check without making changes

**Protocol**:
1. Read `00-FEATURE-OVERVIEW.md`
2. Read `02-IMPLEMENTATION-PLAN.md` (count completed vs total phases)
3. Present status summary (don't modify anything)

**Response template**:
```
Feature: [Name]
Overall: [X]% complete ([Y] of [Z] phases done)
Current Phase: [Phase X - Name]
Last update: [Date from progress log]

Completed:
✓ Phase 1: [Name]
✓ Phase 2: [Name]

In Progress:
~ Phase 3: [Name] ([%] done)

Pending:
- Phase 4: [Name]
- Phase 5: [Name]

Next: [Next task from progress log]
```

---

### `/test`

**Intent**: Start testing phase

**Protocol**:
1. Check if `04-TESTING-CHECKLIST.md` exists
   - If yes: Show existing checklist
   - If no: Create from template
2. Analyze implementation to generate test scenarios:
   - Happy path tests
   - Edge case tests
   - Regression tests (what could break)
3. Populate `04-TESTING-CHECKLIST.md` with scenarios
4. Each scenario needs:
   - Description
   - Steps to reproduce
   - Expected result
   - Status checkbox: [ ] Not Tested

**Response template**:
```
Created 04-TESTING-CHECKLIST.md with [N] test scenarios:

Happy Path:
- Scenario 1: [Description]
- Scenario 2: [Description]

Edge Cases:
- Scenario 3: [Description]
- Scenario 4: [Description]

Regression:
- Scenario 5: [Description]

Ready for testing. Update checklist as you test each scenario.
```

---

### `/bug <description>`

**Intent**: Report and handle a bug

**Protocol**:
1. Append to `03-PROGRESS-LOG.md`:
   ```markdown
   ### 🐛 Bug: [Short description]

   **Reported**: [Date]
   **Description**: [From human]

   **Questions**:
   1. Steps to reproduce?
   2. Expected vs actual behavior?
   3. Error messages or logs?
   ```
2. Ask human for reproduction steps (if not provided)
3. After answers, investigate:
   - Find likely location
   - Analyze root cause
   - Propose fix
4. Update progress log with findings
5. Implement fix (after human approval)

**Response template**:
```
Bug logged in progress log.

Questions to help investigate:
1. [Question 1]
2. [Question 2]
3. [Question 3]

I'll investigate [likely file/area] after your answers.
```

---

### `/archive`

**Intent**: Feature complete, archive old documents

**Protocol**:
1. Verify completion:
   - Check `01-REQUIREMENTS.md` - all checkboxes `[x]`?
   - Check `04-TESTING-CHECKLIST.md` - all tests Pass?
   - Check `02-IMPLEMENTATION-PLAN.md` - all phases `[x]`?
2. If not complete:
   ```
   Cannot archive - feature not complete:
   ❌ [List incomplete items]

   Complete these first, then use /archive
   ```
3. If complete:
   - Create `archive/YYYY-MM-DD-[feature-name]-FINAL.md`
   - Move old session summaries to archive/
   - Keep 5 core docs in root (for reference)
4. Update `00-FEATURE-OVERVIEW.md` status to "Complete"

**Response template**:
```
Verifying completion...
✓ All requirements met
✓ All tests passing
✓ All phases complete

Created: archive/2025-MM-DD-[feature]-FINAL.md
Moved to archive: [list]
Kept in root: 5 core documents

Feature complete! 🎉
```

---

## Session Workflow

### Starting New Session (After Break)

When human says `/continue`:

1. **Read SSOT**: `00-FEATURE-OVERVIEW.md`
   - Feature name
   - Overall status
   - Current phase
2. **Read Progress Log**: Last entry in `03-PROGRESS-LOG.md`
   - What was last completed
   - What's next
3. **Summarize**: 3-4 sentences max
4. **Confirm**: State next task specifically
5. **Wait**: For human approval

**Template**:
```
Feature: [Name]
Status: [From SSOT]
Phase: [Current phase name]
Last: [Last completed item]
Next: [Specific task with file:line if applicable]

Ready to proceed?
```

### During Work

**For each change**:
1. Read relevant files
2. Make changes
3. Explain what was done (concisely)
4. Update relevant docs

**After each phase**:
1. Mark phase `[x]` in `02-IMPLEMENTATION-PLAN.md`
2. Append summary to `03-PROGRESS-LOG.md`
3. Ask human to verify before next phase

**For bugs/issues**:
1. Append to `03-PROGRESS-LOG.md` under "Issues"
2. Analyze root cause
3. Fix
4. Update log with resolution

### Ending Session

When human says `/wrap`:

1. **Update Plan**: Mark completed phases
2. **Update Progress Log**: Append session summary with handoff
3. **Update SSOT**: If milestone reached
4. **Summarize**: What was done + what's next

**Never**:
- Create new summary documents
- Duplicate info across files
- Leave vague "continue later" notes
- Skip the handoff

---

## Document Management Rules

### Max Lengths (Enforce These)

| Document | Max Length | Action if Exceeded |
|----------|-----------|-------------------|
| 00-FEATURE-OVERVIEW.md | 2 pages | Refactor, archive old decisions |
| 01-REQUIREMENTS.md | 3 pages | Split feature or remove detail |
| 02-IMPLEMENTATION-PLAN.md | 4 pages | Break phases into sub-features |
| 03-PROGRESS-LOG.md | Unlimited | Archive old entries (keep recent) |
| 04-TESTING-CHECKLIST.md | 2 pages | Remove duplicate scenarios |

### Append-Only Rule

`03-PROGRESS-LOG.md` is **append-only**:
- ✅ Add new entries at the end
- ❌ Never modify old entries (except typos)
- ❌ Never create separate session summary files
- ❌ Never duplicate info already in the log

### SSOT Updates

`00-FEATURE-OVERVIEW.md` should be updated only when:
- Phase changes
- Status changes (Planning → Implementation → Testing → Complete)
- Major decision changes
- Current blockers change

**Don't update for**: Every small progress (that goes in progress log)

---

## Communication Guidelines

### Be Concise

**Good** ✅:
```
Fixed pointsAvailable in exam.service.ts:183
Added getPointsAvailableForQuizSession() method
Tests passing
```

**Bad** ❌:
```
I have successfully implemented a comprehensive solution to address
the complex issue regarding the pointsAvailable field calculation by
creating a new helper method that properly handles both standard and
practice exam types through sophisticated logic that...
[continues for 3 paragraphs]
```

### Be Specific

**Good** ✅:
```
Next: Implement NotificationService.send() in src/services/notification.service.ts
Add email template rendering using existing TemplateEngine class
```

**Bad** ❌:
```
Next: Continue working on the notification feature
```

### Confirm Before Major Actions

**Good** ✅:
```
I'll refactor these 5 files to implement the new strategy:
- file1.ts
- file2.ts
- file3.ts
- file4.ts
- file5.ts

This affects [X functionality]. Proceed?
```

**Bad** ❌:
```
[Immediately refactors without asking]
```

### Link, Don't Duplicate

**Good** ✅:
```
See requirements in 01-REQUIREMENTS.md section "Edge Cases"
```

**Bad** ❌:
```
The requirements state that we need to handle edge cases:
1. [copies entire edge case section]
2. ...
```

---

## Error Handling

### If Documents Don't Exist

On `/continue` if core docs missing:
```
Error: Core documents not found.

Use /start [feature-name] to initialize a new feature first.
```

### If Requirements Incomplete

On `/test` or implementation if requirements unclear:
```
Cannot proceed - requirements incomplete.

Missing information:
- [Item 1]
- [Item 2]

Please update 01-REQUIREMENTS.md or answer these questions:
[Questions]
```

### If Tests Failing

Don't mark feature complete:
```
Cannot archive - tests failing:

❌ Test 3: [Description] (see 04-TESTING-CHECKLIST.md)
❌ Test 5: [Description]

Fix these issues first, then use /archive
```

---

## Templates Location

Templates for core documents are in `meta-v2/templates/`:
- `00-FEATURE-OVERVIEW.md`
- `01-REQUIREMENTS.md`
- `02-IMPLEMENTATION-PLAN.md`
- `03-PROGRESS-LOG.md`
- `04-TESTING-CHECKLIST.md`

When creating new documents, copy template and fill in content.

---

## Anti-Patterns (Never Do These)

❌ Creating multiple status documents
❌ Recreating session summaries instead of appending
❌ Starting work without reading SSOT
❌ Vague handoffs ("continue the feature")
❌ Documents exceeding max length
❌ Duplicating information across documents
❌ Assuming context from previous session
❌ Making major changes without approval

---

## Success Criteria

You're following the protocol correctly if:

✅ Every session starts by reading SSOT
✅ Progress log grows by appending (never recreating)
✅ Handoffs include specific next task with file path
✅ Documents stay within max length
✅ Human can resume work in < 2 minutes
✅ Only 5 core docs exist (plus archive)
✅ No duplicate summaries

---

## Quick Reference

| Human Says | You Do |
|-----------|--------|
| `/start X` | Create SSOT + requirements, ask questions |
| `/continue` | Read SSOT + log, confirm next task |
| `/wrap` | Update plan + log, summarize session |
| `/status` | Show current progress (no changes) |
| `/test` | Create test checklist |
| `/bug X` | Log bug, ask questions, investigate |
| `/archive` | Verify complete, create final summary |

**Always**: Read SSOT first, be specific, confirm major changes, respect limits.

**Never**: Create new summaries, duplicate info, exceed max lengths, skip handoffs.

---

This is your complete protocol. Follow it precisely for consistent, efficient collaboration with humans.
