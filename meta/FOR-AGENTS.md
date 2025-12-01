# Protocol for AI Agents

**Purpose**: This document defines how you should operate when working on features using this system.

**When to read this**: Human will point you here with: "Use meta system" or "Read meta/FOR-AGENTS.md"

---

## Core Principles

1. **SSOT First**: Always read `00-FEATURE-OVERVIEW.md` before anything else
2. **Append, Don't Recreate**: Add to `03-PROGRESS-LOG.md`, never create new summaries
3. **Respect Limits**: Documents have max lengths - enforce them
4. **Be Specific**: File paths, line numbers, exact next tasks
5. **Confirm Major Changes**: Ask before refactoring, big changes
6. **Be Concise**: Prioritize being concise over verbose descriptions
7. **Update Checkboxes**: ALWAYS mark checkboxes `[x]` when tasks/tests/requirements are completed

---

## Project Structure

The meta system organizes work in this structure:

```
project-root/ai-agent/
├── meta/                           ← System documentation (read-only)
│   ├── FOR-AGENTS.md              ← This file
│   ├── FOR-HUMANS.md
│   ├── README.md
│   └── templates/
│       ├── features/              ← Feature templates
│       └── knowledge/             ← Knowledge templates
├── features/                       ← Active feature work
│   ├── 001_feature-name/
│   │   ├── 00-FEATURE-OVERVIEW.md
│   │   ├── 01-REQUIREMENTS.md
│   │   ├── 02-IMPLEMENTATION-PLAN.md
│   │   ├── 03-PROGRESS-LOG.md
│   │   └── 04-TESTING-CHECKLIST.md
│   └── 002_another-feature/
│       └── [same 5 documents]
└── knowledge/                      ← Project knowledge base
    ├── SYSTEM-OVERVIEW.md
    ├── REPOSITORY-MAP.md
    ├── CONCEPTS-INDEX.md
    └── subsystems/
        └── [subsystem].md
```

## The 5 Core Documents (Per Feature)

Each feature has its own folder in `ai-agent/features/NNN_feature-name/`:

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

When human uses meta-instructions (shortcuts starting with `>>`), follow these protocols:

### `>>start <feature-name>`

**Intent**: Initialize new feature

**Protocol**:
1. **Check knowledge base** (CRITICAL - Do this first):
   - Read `ai-agent/knowledge/SYSTEM-OVERVIEW.md` if it exists
   - Check `ai-agent/knowledge/CONCEPTS-INDEX.md` for relevant patterns
   - Look for related subsystem notes in `knowledge/subsystems/`
   - Use this context to ask better questions and understand requirements

2. **Determine feature number**:
   - Check `ai-agent/features/` for existing feature folders
   - Find highest number (e.g., 003)
   - Next number is highest + 1 (e.g., 004)
   - If no features exist, start with 001
2. **Create feature folder**: `ai-agent/features/NNN_feature-name/`
   - Use 3-digit number (001, 002, etc.)
   - Use kebab-case for feature name
   - Example: `ai-agent/features/004_user-authentication/`
3. **Copy and customize templates** from `meta/templates/features/`:
   - `00-FEATURE-OVERVIEW.md`:
     - Set feature name
     - Set status: "Planning"
     - Set started date
   - `01-REQUIREMENTS.md`:
     - Add obvious requirements from human's description
     - Add 3-5 clarifying questions (informed by knowledge base)
4. **Present questions** to human (questions should reference project context from knowledge)
5. **Wait for answers** (don't proceed to implementation yet)

**Response template**:
```
I'll create the foundation for [feature-name].

Created feature folder: ai-agent/features/NNN_feature-name/

Created:
- 00-FEATURE-OVERVIEW.md (draft)
- 01-REQUIREMENTS.md (draft)

Questions about requirements:
1. [Question 1]
2. [Question 2]
3. [Question 3]

Please answer these so I can create an implementation plan.
```

**Next steps**: After human answers → Create `02-IMPLEMENTATION-PLAN.md` in feature folder → Wait for approval

---

### `>>continue`

**Intent**: Resume work on existing feature

**Protocol**:
1. **Check knowledge base** (Do this first):
   - Review `ai-agent/knowledge/SYSTEM-OVERVIEW.md` for project context
   - Check for relevant subsystem notes in `knowledge/subsystems/`
   - This helps you understand the codebase before diving in

2. **Read feature SSOT**: `00-FEATURE-OVERVIEW.md`
   - Extract: feature name, current status, current phase

3. **Read last entry** in `03-PROGRESS-LOG.md`
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

### `>>wrap`

**Intent**: End session with proper handoff

**Protocol**:
1. Update `02-IMPLEMENTATION-PLAN.md`:
   - Mark any completed phases with `[x]` (CRITICAL: Always update checkboxes)
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

   Quick start: ">>continue"
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

### `>>status`

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

### `>>test`

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
   - Status checkbox: [ ] Not Tested (UPDATE to [x] when test passes)

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

### `>>bug <description>`

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

### `>>archive`

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

When human says `>>continue`:

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
1. Check knowledge base for relevant subsystem info
2. Read relevant files
3. Make changes
4. Explain what was done (concisely)
5. Update relevant docs

**After each phase**:
1. Mark phase `[x]` in `02-IMPLEMENTATION-PLAN.md` (CRITICAL: Don't forget this step)
2. Append summary to `03-PROGRESS-LOG.md`
3. **Consider knowledge updates**: Did you discover patterns worth documenting?
4. Ask human to verify before next phase

**For bugs/issues**:
1. Append to `03-PROGRESS-LOG.md` under "Issues"
2. Check knowledge base for relevant subsystem info
3. Analyze root cause
4. Fix
5. Update log with resolution
6. **Update knowledge** if gotcha is worth documenting

### Ending Session

When human says `>>wrap`:

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

On `>>continue` if core docs missing:
```
Error: Core documents not found.

Use >>start [feature-name] to initialize a new feature first.
```

### If Requirements Incomplete

On `>>test` or implementation if requirements unclear:
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

Fix these issues first, then use >>archive
```

---

### `>>init-knowledge`

**Intent**: Initialize project knowledge base (human + QnA combined)

**Protocol**:
1. **Check for existing knowledge**:
   - Look for `ai-agent/knowledge/SYSTEM-OVERVIEW.md`
   - If exists: Read it and identify gaps
   - If doesn't exist: Note that full QnA is needed

2. **Prepare QnA questions**:
   - Review what human already provided
   - Generate questions for missing information:
     - Project purpose (if not clear)
     - Domain context (if not mentioned)
     - Tech stack details (if incomplete)
     - Architecture patterns (if not described)
     - Key conventions (if not documented)
     - Development workflow (if not explained)
     - Known gotchas (if not listed)

3. **Conduct QnA session**:
   - Present questions to human
   - Wait for answers
   - Clarify anything ambiguous

4. **Create/Update SYSTEM-OVERVIEW.md**:
   - Merge human-provided content + QnA answers
   - Fill template completely
   - Save to `ai-agent/knowledge/SYSTEM-OVERVIEW.md`

5. **Confirm completion**:
   - Summarize what was captured
   - Suggest running `>>scan-repo` next

**Response template**:
```
I'll help set up your project knowledge base.

[If SYSTEM-OVERVIEW.md exists:]
I found your existing system overview. Let me ask a few questions to fill in the gaps:

[If SYSTEM-OVERVIEW.md doesn't exist:]
I'll ask some questions to understand your project:

Questions:
1. [Question 1]
2. [Question 2]
...

[After answers:]
Created/Updated: ai-agent/knowledge/SYSTEM-OVERVIEW.md

Captured:
- Project purpose and domain
- Tech stack: [summary]
- Architecture: [summary]
- Key conventions: [count] documented

Next: Run >>scan-repo to map the codebase structure.
```

**Next steps**: Human can run `>>scan-repo` or start first feature

---

### `>>scan-repo`

**Intent**: Scan repository and generate knowledge maps

**Protocol**:
1. **Scan directory structure**:
   - Map folders and key files
   - Identify entry points (main, server, CLI)
   - Find configuration files
   - Note build and test setup

2. **Create REPOSITORY-MAP.md**:
   - Document directory structure
   - List key files by category
   - Identify main workflows
   - Note file counts and technologies

3. **Analyze code patterns**:
   - Scan for data models/schemas
   - Find API endpoints/routes
   - Identify utilities and helpers
   - Note design patterns
   - Find authentication/authorization setup

4. **Create CONCEPTS-INDEX.md**:
   - Catalog discovered patterns
   - List data models with locations
   - Document API structure
   - Note common abstractions
   - Link to relevant files

5. **Confirm completion**:
   - Summarize what was found
   - Suggest starting first feature

**Response template**:
```
Scanning repository structure...

Created: ai-agent/knowledge/REPOSITORY-MAP.md
- [X] directories mapped
- [Y] entry points found
- [Z] main workflows documented

Created: ai-agent/knowledge/CONCEPTS-INDEX.md
- [N] data models cataloged
- [M] API endpoints mapped
- [P] patterns identified

Key findings:
- Architecture: [detected type]
- Entry point: [main file]
- Test framework: [detected framework]

Your knowledge base is ready! Use >>start [feature-name] to begin.
```

**Notes**:
- This can be token-intensive for large repos
- Focus on high-value information
- Don't document every file
- Can be run multiple times as project evolves

---

## Knowledge System

The knowledge system helps you understand and document the project.

### Knowledge Structure

```
ai-agent/knowledge/
├── SYSTEM-OVERVIEW.md      ← High-level project info (human or QnA)
├── REPOSITORY-MAP.md       ← Auto-generated from repo scan
├── CONCEPTS-INDEX.md       ← Catalog of patterns, APIs, models
└── subsystems/
    ├── auth.md            ← Incremental subsystem notes
    ├── database.md
    └── api.md
```

### When to Use Knowledge

**Before starting a feature**:
1. Read `SYSTEM-OVERVIEW.md` for project context
2. Check `CONCEPTS-INDEX.md` for relevant patterns
3. Look for related subsystem notes in `knowledge/subsystems/`

**During feature development**:
1. When discovering important patterns → Update `CONCEPTS-INDEX.md`
2. When working deeply in a subsystem → Create/update subsystem note
3. Keep updates lightweight - focus on reusable insights

**After repository scan**:
1. Generate `REPOSITORY-MAP.md` with directory structure
2. Generate `CONCEPTS-INDEX.md` with discovered patterns
3. Reference specific file locations

### Knowledge Workflows

#### Initial Knowledge: Combined Approach

**When**: Project setup, before first feature (via `>>init-knowledge`)
**Template**: `meta/templates/knowledge/SYSTEM-OVERVIEW.md`

**Combined Human + QnA Approach**:

The best approach combines human-provided information AND agent QnA:

1. **Human provides initial knowledge** (optional):
   - Creates `ai-agent/knowledge/SYSTEM-OVERVIEW.md`
   - Fills in what they know (partial is fine!)
   - Can skip sections they're unsure about

2. **Agent reads and identifies gaps**:
   - Reads any existing SYSTEM-OVERVIEW.md
   - Identifies missing or unclear information
   - Prepares targeted questions

3. **Agent conducts QnA**:
   - Asks questions only about missing information
   - Clarifies ambiguous points
   - Fills in gaps from human's answers

4. **Agent merges everything**:
   - Combines human-provided + QnA answers
   - Creates comprehensive SYSTEM-OVERVIEW.md
   - No redundancy, just complete information

**QnA Questions Example** (asked only for missing info):
```
1. What does this project do? What problem does it solve?
2. What domain is this in? (e.g., e-commerce, fintech, education)
3. What's the tech stack? (language, framework, database)
4. What's the high-level architecture? (monolith, microservices, etc.)
5. What are the major components or subsystems?
6. Are there important conventions or patterns I should know?
7. How do developers typically run this locally?
8. Are there any known gotchas or quirks?
```

#### Repository Scanning

**When**: After initial setup, before deep feature work
**Templates**: `REPOSITORY-MAP.md`, `CONCEPTS-INDEX.md`

**Protocol**:
1. Scan directory structure → Document in `REPOSITORY-MAP.md`
2. Identify entry points (main files, servers, CLI tools)
3. Find configuration files
4. Map major workflows (auth, data processing, etc.)
5. Catalog patterns in `CONCEPTS-INDEX.md`:
   - Data models and schemas
   - API endpoints
   - Common utilities
   - Design patterns
6. Note file counts and technology detection

**Keep it focused**: Don't document everything, focus on:
- Entry points and main workflows
- Repeated patterns
- Key abstractions
- Important dependencies

#### Incremental Knowledge During Features

**When**: While working on a feature, when you discover something valuable
**Template**: `meta/templates/knowledge/subsystems/TEMPLATE.md`

**Protocol**:
1. **Recognize when to document**:
   - You're working deeply in a specific subsystem
   - You discover non-obvious patterns
   - You find gotchas worth noting
   - You understand a complex workflow

2. **Create/update subsystem note**:
   - Check if `knowledge/subsystems/[name].md` exists
   - If not, copy template and fill in
   - If yes, add to "Recent Changes" section

3. **Keep it brief**:
   - Purpose of the subsystem
   - Key files and their roles
   - Important patterns or gotchas
   - Related subsystems

4. **Update feature progress log**:
   ```markdown
   **Knowledge Updated**:
   - Created/Updated: knowledge/subsystems/[name].md
   - Added: [Brief description of what was documented]
   ```

**Don't over-document**:
- Not every file needs documentation
- Focus on insights that will help future work
- Skip obvious or self-explanatory code
- Prioritize gotchas and non-obvious patterns

### Knowledge Best Practices

✅ **Do**:
- Read knowledge docs before starting features
- Update when you discover valuable insights
- Keep subsystem notes focused and brief
- Link between related subsystems
- Note file locations with `file:line` format

❌ **Don't**:
- Document everything exhaustively
- Duplicate information between knowledge files
- Create knowledge docs for obvious code
- Let knowledge docs get stale (mark "Last Updated")
- Spend more time documenting than coding

---

## Templates Location

Templates are organized by type in `meta/templates/`:

### Feature Templates
`meta/templates/features/`:
- `00-FEATURE-OVERVIEW.md`
- `01-REQUIREMENTS.md`
- `02-IMPLEMENTATION-PLAN.md`
- `03-PROGRESS-LOG.md`
- `04-TESTING-CHECKLIST.md`

### Knowledge Templates
`meta/templates/knowledge/`:
- `SYSTEM-OVERVIEW.md` - High-level project information
- `REPOSITORY-MAP.md` - Auto-generated repository structure
- `CONCEPTS-INDEX.md` - Catalog of patterns and concepts
- `subsystems/TEMPLATE.md` - Template for subsystem documentation

When creating new documents, copy appropriate template and fill in content.

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

✅ Every session starts by reading SSOT from the feature folder
✅ Features are in numbered folders (001_, 002_, etc.)
✅ Progress log grows by appending (never recreating)
✅ Handoffs include specific next task with file path
✅ Documents stay within max length
✅ Human can resume work in < 2 minutes
✅ Only 5 core docs per feature (plus archive)
✅ Knowledge docs updated when valuable insights discovered
✅ No duplicate summaries

---

## Quick Reference

| Human Says | You Do |
|-----------|--------|
| `>>init-knowledge` | Setup knowledge base: read existing overview, QnA for gaps, merge info |
| `>>scan-repo` | Scan codebase, generate REPOSITORY-MAP and CONCEPTS-INDEX |
| `>>start X` | Check knowledge base, create numbered feature folder, ask questions |
| `>>continue` | Check knowledge base, read SSOT from feature folder, confirm next task |
| `>>wrap` | Update plan + log, consider knowledge updates, summarize session |
| `>>status` | Show current progress (no changes) |
| `>>test` | Create test checklist |
| `>>bug X` | Log bug, check knowledge, investigate, update knowledge if needed |
| `>>archive` | Verify complete, create final summary |

**Always**: Check knowledge base first, read SSOT, be specific, confirm major changes, respect limits, update checkboxes, document valuable insights.

**Never**: Skip knowledge lookup, create new summaries, duplicate info, exceed max lengths, skip handoffs, forget to number features, ignore discovered patterns.

---

This is your complete protocol. Follow it precisely for consistent, efficient collaboration with humans.
