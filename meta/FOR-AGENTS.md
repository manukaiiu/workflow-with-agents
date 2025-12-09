# Protocol for AI Agents

**Purpose**: This document defines how you should operate when working on features using this system.

**When to read this**:
- **First session**: Human will say: "Please read ai-agent/meta/FOR-AGENTS.md - this explains our workflow system."
- **After context loss** (window closed, crash, new session): Human will say: "Please read ai-agent/meta/FOR-AGENTS.md to understand our workflow system, then >>continue"
- **During work**: Reference this as needed for specific workflows

**After reading this**: You'll understand the `>>` command system and can start working with `>>init-knowledge` or `>>start`

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
│       ├── maintenance/           ← Maintenance templates
│       ├── concept/               ← Concept workflow templates
│       └── knowledge/             ← Knowledge templates
├── work/                           ← Active work (features, maintenance, bugs, concepts)
│   ├── 001-feat-user-auth/        ← Feature work
│   │   ├── 00-OVERVIEW.md
│   │   ├── 01-REQUIREMENTS.md
│   │   ├── 02-IMPLEMENTATION-PLAN.md
│   │   ├── 03-PROGRESS-LOG.md
│   │   ├── 04-TESTING-CHECKLIST.md
│   │   ├── 05-ANALYSIS.md         ← Optional: feature-specific research
│   │   └── 06-PR-MESSAGE.md       ← Optional: PR draft
│   ├── 002-maint-deps-update/     ← Maintenance work
│   │   └── [maintenance documents]
│   ├── 003-bug-login-fix/         ← Bug fix work
│   │   └── [feature documents]
│   └── 004-concept-new-platform/  ← Concept work (during creation)
│       ├── 00-OVERVIEW.md
│       ├── 01-INPUTS/INDEX.md
│       ├── 02-EXTRACTIONS.md
│       ├── 03-CONCEPT.md
│       └── [other concept docs]
├── concepts/                       ← Finalized concepts (after >>finalize)
│   └── [name]/v1/
│       ├── CONCEPT.md
│       └── CONCEPT-[sub].md
├── workplans/                      ← Finalized work plans (after >>finalize)
│   └── [name]/v1/
│       ├── WORKPLAN.md
│       ├── ROADMAP.md
│       └── ROADMAP.mermaid.md
└── knowledge/                      ← Project knowledge base
    ├── SYSTEM-OVERVIEW.md
    ├── REPOSITORY-MAP.md
    ├── CONCEPTS-INDEX.md
    ├── COMMANDS.md                ← Project-specific commands
    └── subsystems/
        └── [subsystem].md
```

## Work Types

The system supports four work types, each with its own folder prefix:

| Type | Prefix | Use For | Templates |
|------|--------|---------|-----------|
| Feature | `feat` | New functionality, enhancements | `templates/features/` |
| Maintenance | `maint` | Dependency updates, refactoring, security audits, build changes | `templates/maintenance/` |
| Bug | `bug` | Bug fixes | `templates/features/` (lighter usage) |
| Concept | `concept` | Complex conceptualization, work plans, roadmaps | `templates/concept/` |

**Folder naming**: `NNN-TYPE-name` (e.g., `001-feat-user-auth`, `002-maint-deps-update`, `003-bug-login-fix`, `004-concept-new-platform`)

**Note**: Concept work has a unique lifecycle - it starts in `work/` during creation, then finalized outputs are promoted to top-level `concepts/` and `workplans/` folders.

## Core Documents

Each work item has its own folder in `ai-agent/work/NNN-TYPE-name/`:

### Required Documents (All Work Types)
```
00-OVERVIEW.md             ← SSOT - read this FIRST every session
02-IMPLEMENTATION-PLAN.md  ← How to build (max 4 pages, phase-based)
03-PROGRESS-LOG.md         ← Session log (append-only, unlimited)
04-TESTING-CHECKLIST.md    ← Test scenarios (max 2 pages)
```

### Additional Documents by Work Type

**Features (`feat`)** - Full documentation:
```
01-REQUIREMENTS.md         ← What to build (max 3 pages)
05-ANALYSIS.md             ← Optional: feature-specific research
06-PR-MESSAGE.md           ← Optional: PR draft (maintained throughout)
```

**Maintenance (`maint`)** - Lighter documentation:
```
01-SCOPE.md                ← What's included, compatibility concerns (max 2 pages)
```

**Bugs (`bug`)** - Use feature templates, focus on:
```
01-REQUIREMENTS.md         ← Bug description, reproduction, expected behavior
```

**Concepts (`concept`)** - Full conceptualization workflow:
```
00-OVERVIEW.md             ← SSOT for concept work status
01-INPUTS/INDEX.md         ← Inventory of all inputs
02-EXTRACTIONS.md          ← Extracted information from inputs
03-CONCEPT.md              ← Main concept document
03-CONCEPT-[sub].md        ← Sub-concept documents (max 7)
04-WORKPLAN.md             ← Work breakdown structure
05-ROADMAP.md              ← Sequencing and dependencies
05-ROADMAP.mermaid.md      ← Generated Mermaid visualization
06-PROGRESS-LOG.md         ← Session log (append-only)
07-REFINEMENT-LOG.md       ← Tracks refinement cycles
08-OPEN-QUESTIONS.md       ← Questions awaiting human input
```

**Never create other status/summary documents**. If info doesn't fit in these docs, it goes in `03-PROGRESS-LOG.md` (or `06-PROGRESS-LOG.md` for concepts).

---

## Meta-Instruction Handlers

When human uses meta-instructions (shortcuts starting with `>>`), follow these protocols:

### `>>start [TYPE] <name>`

**Intent**: Initialize new work item (feature, maintenance, or bug)

**Syntax**:
- `>>start feat user-auth` - New feature
- `>>start maint deps-update` - Maintenance work
- `>>start bug login-issue` - Bug fix
- `>>start my-feature` - Defaults to `feat` if type omitted

**Protocol**:

1. **Check knowledge base** (CRITICAL - Do this first):
   - Read `ai-agent/knowledge/SYSTEM-OVERVIEW.md` if it exists
   - Check `ai-agent/knowledge/CONCEPTS-INDEX.md` for relevant patterns
   - Check `ai-agent/knowledge/COMMANDS.md` for project commands
   - Look for related subsystem notes in `knowledge/subsystems/`
   - Use this context to ask better questions and understand requirements

2. **Ensure work directory exists**:
   - If `ai-agent/work/` doesn't exist, create it: `mkdir -p ai-agent/work`

3. **Determine work item number** (CRITICAL - follow exactly):
   - List all folders in `ai-agent/work/`
   - Extract the numeric prefix from each folder (e.g., `001` from `001-feat-auth`)
   - Find the HIGHEST number across ALL folders regardless of type
   - Next number = highest + 1
   - If no folders exist, start with 001
   - **Example**: If folders are `001-feat-auth`, `002-maint-deps`, `003-bug-fix`, next is `004`

4. **Create work folder**: `ai-agent/work/NNN-TYPE-name/`
   - Use 3-digit number (001, 002, etc.)
   - Use work type prefix (feat, maint, bug)
   - Use kebab-case for name
   - Example: `ai-agent/work/004-feat-user-notifications/`

5. **Copy and customize templates** based on work type:

   **For `feat` (features)**:
   - Copy from `meta/templates/features/`
   - `00-OVERVIEW.md`: Set name, status "Planning", date
   - `01-REQUIREMENTS.md`: Add obvious requirements, 3-5 questions

   **For `maint` (maintenance)**:
   - Copy from `meta/templates/maintenance/`
   - `00-OVERVIEW.md`: Set name, status "Planning", date
   - `01-SCOPE.md`: Define scope, compatibility concerns

   **For `bug` (bugs)**:
   - Copy from `meta/templates/features/`
   - `00-OVERVIEW.md`: Set name, status "Investigating", date
   - `01-REQUIREMENTS.md`: Bug description, reproduction steps, expected behavior

6. **Research and document** (NEW - knowledge capture):
   - If you research the codebase during planning, document findings
   - Update `knowledge/CONCEPTS-INDEX.md` with discovered patterns
   - Create/update subsystem docs if you learn significant details
   - Note in progress log: "Knowledge updated: [what was added]"

7. **Present questions** to human (informed by knowledge base research)
8. **Wait for answers** (don't proceed to implementation yet)

**Response template**:
```
I'll create the foundation for [TYPE]: [name].

Created work folder: ai-agent/work/NNN-TYPE-name/

Created:
- 00-OVERVIEW.md (draft)
- 01-REQUIREMENTS.md / 01-SCOPE.md (draft)

[If knowledge was updated:]
Updated knowledge:
- CONCEPTS-INDEX.md: Added [pattern/concept]

Questions about [requirements/scope]:
1. [Question 1]
2. [Question 2]
3. [Question 3]

Please answer these so I can create an implementation plan.
```

**Next steps**: After human answers → Create `02-IMPLEMENTATION-PLAN.md` → Wait for approval

---

### `>>continue`

**Intent**: Resume work on existing work item

**Protocol**:
1. **Check knowledge base** (Do this first):
   - Review `ai-agent/knowledge/SYSTEM-OVERVIEW.md` for project context
   - Check `ai-agent/knowledge/COMMANDS.md` for project commands
   - Check for relevant subsystem notes in `knowledge/subsystems/`
   - This helps you understand the codebase before diving in

2. **Find active work item**:
   - List folders in `ai-agent/work/`
   - If multiple exist, check which has status "In Progress" in `00-OVERVIEW.md`
   - If unclear, ask human which work item to continue

3. **Read work SSOT**: `00-OVERVIEW.md`
   - Extract: work name, type, current status, current phase

4. **Read last entry** in `03-PROGRESS-LOG.md`
   - Extract: last completed item, next task

5. Summarize understanding (max 4 sentences)
6. State specific next task
7. Ask for confirmation

**Response template**:
```
Work: [Name from SSOT] (TYPE)
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

2. **Knowledge checkpoint** (CRITICAL - do this before logging):
   - Did you discover patterns worth documenting? → Update `CONCEPTS-INDEX.md`
   - Were there gotchas future agents should know? → Update relevant subsystem doc
   - Did you learn useful commands? → Update `COMMANDS.md`
   - Any significant codebase insights? → Create/update subsystem doc

3. Append to `03-PROGRESS-LOG.md`:
   ```markdown
   ## [YYYY-MM-DD] Session N

   **Duration**: [X hours/minutes]
   **Phase**: [Current phase]

   **Completed**:
   - [x] Item 1
   - [x] Item 2

   **Issues Encountered & Resolved**:
   - Issue: [desc] → Solution: [desc] → Location: file.ts:line

   **Knowledge Updated**:
   - [List any knowledge docs updated, or "None"]

   **Next Session Start Here**:
   Priority 1: [Most important next task]
   Priority 2: [Second task]

   Context: [Any specific knowledge needed]
   Files: [Files to review]

   Quick start: ">>continue"
   ```

4. Update `00-OVERVIEW.md` if major milestone reached
5. Update `06-PR-MESSAGE.md` if it exists (keep PR draft current)
6. Summarize session to human

**Response template**:
```
Session summary:
✓ Completed: [List]
✓ Tests: [Status]
✓ Knowledge: [Updated X / No updates needed]

Updated:
- 03-PROGRESS-LOG.md (with handoff)
- 02-IMPLEMENTATION-PLAN.md (marked Phase X complete)
- [Any knowledge docs updated]

Next session: [Specific next task]
```

---

### `>>status`

**Intent**: Quick status check without making changes

**Protocol**:
1. Read `00-OVERVIEW.md`
2. Read `02-IMPLEMENTATION-PLAN.md` (count completed vs total phases)
3. Present status summary (don't modify anything)

**Response template**:
```
Work: [Name] (TYPE)
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

**Intent**: Work complete, archive old documents

**Protocol**:
1. Verify completion:
   - Check `01-REQUIREMENTS.md` or `01-SCOPE.md` - all checkboxes `[x]`?
   - Check `04-TESTING-CHECKLIST.md` - all tests Pass?
   - Check `02-IMPLEMENTATION-PLAN.md` - all phases `[x]`?
2. If not complete:
   ```
   Cannot archive - work not complete:
   ❌ [List incomplete items]

   Complete these first, then use >>archive
   ```
3. If complete:
   - Create `archive/YYYY-MM-DD-[name]-FINAL.md`
   - Move old session summaries to archive/
   - Keep core docs in folder (for reference)
4. Update `00-OVERVIEW.md` status to "Complete"

**Response template**:
```
Verifying completion...
✓ All requirements/scope met
✓ All tests passing
✓ All phases complete

Created: archive/2025-MM-DD-[name]-FINAL.md
Moved to archive: [list]
Kept in folder: core documents

Work complete! 🎉
```

---

### `>>checkpoint`

**Intent**: Capture knowledge before context compression (use proactively at ~70-80% context)

**When to use**:
- Long sessions approaching context limits
- Before expected context compression/summarization
- When you've accumulated significant insights not yet documented
- Human explicitly requests knowledge capture

**Protocol**:
1. **Review session activity**:
   - What patterns have you discovered?
   - What gotchas or issues were encountered?
   - What commands or workflows were useful?
   - What subsystem knowledge was gained?

2. **Update knowledge docs**:
   - `CONCEPTS-INDEX.md`: New patterns, APIs, models discovered
   - `COMMANDS.md`: Useful commands learned
   - `subsystems/[name].md`: Deep subsystem insights
   - `SYSTEM-OVERVIEW.md`: High-level architecture insights (rare)

3. **Update progress log**:
   ```markdown
   ### 📸 Knowledge Checkpoint

   **Captured**:
   - [What was documented]
   - [Where it was added]

   **Context for continuation**:
   - Current task: [What you're working on]
   - Key files: [Files currently relevant]
   - Pending decisions: [Any open questions]
   ```

4. **Summarize to human**:
   ```
   Knowledge checkpoint captured.

   Updated:
   - [List of knowledge docs updated]

   Current context preserved for continuation.
   Ready to proceed.
   ```

**Note**: This does NOT end the session. Continue working after checkpoint.

---

## Concept Workflow Commands

The concept workflow is for complex conceptualization work that involves analyzing inputs, building concepts, creating work plans, and generating roadmaps.

### Intelligent Command Detection

**Agent Behavior**: When human provides input without an explicit `>>` command:
1. Analyze the prompt for intent
2. If it matches a command purpose with confidence, follow that workflow
3. If uncertain, ask: "This sounds like you want to [action]. Should I proceed with `>>[command]`?"

**Examples**:
- "Here's a PDF about the requirements" → Treat as `>>add-input`
- "Let's think through what this system needs to do" → Treat as `>>conceptualize`
- "Can you break this down into tasks?" → Treat as `>>plan`

---

### `>>start concept <name>`

**Intent**: Initialize new concept work

**Protocol**:

1. **Check knowledge base** (as with other work types)

2. **Ensure directories exist**:
   - `mkdir -p ai-agent/work`

3. **Determine work item number** (same protocol as other types)

4. **Create concept work folder**: `ai-agent/work/NNN-concept-name/`
   - Create `01-INPUTS/` subfolder

5. **Copy and customize templates** from `meta/templates/concept/`:
   - `00-OVERVIEW.md`: Set name, status "Gathering", date
   - `01-INPUTS/INDEX.md`: Empty inventory
   - `08-OPEN-QUESTIONS.md`: Template ready for questions

6. **Ask about input sources**:
   - What raw inputs will be analyzed?
   - Are there URLs, files, or documents to process?
   - What format are they in?

7. **Checkpoint consideration**: After creating structure, assess if checkpoint needed

**Response template**:
```
I'll create the foundation for concept: [name].

Created work folder: ai-agent/work/NNN-concept-name/

Created:
- 00-OVERVIEW.md (status: Gathering)
- 01-INPUTS/INDEX.md (empty)
- 08-OPEN-QUESTIONS.md (ready)

Questions about inputs:
1. What raw inputs will we analyze? (conversations, documents, PDFs?)
2. Are there URLs to fetch or files to add?
3. Any specific areas to focus on?

Use >>add-input [path/url] to add input sources.
```

---

### `>>add-input <path-or-url>`

**Intent**: Add input source to concept work

**Protocol**:

1. **Determine input type**:
   - URL: Fetch content and save locally to `01-INPUTS/`
   - Local file: Copy to `01-INPUTS/`
   - PDF: Attempt extraction, ask human to confirm accuracy

2. **Add entry to `01-INPUTS/INDEX.md`**:
   ```markdown
   ## [Input Name]
   - **Source**: [path or URL]
   - **Type**: conversation | document | pdf | web | other
   - **Size**: [lines/pages/words estimate]
   - **Added**: [date]
   - **Status**: [ ] Not processed
   - **Processing Notes**: [Any issues or considerations]
   - **Summary**: [Brief description - filled after extraction]
   ```

3. **Update `00-OVERVIEW.md`** input count

4. **Large Input Handling** (10000+ lines):
   - Do NOT summarize or skip content
   - Note in INDEX.md: "Large input - will process in chunks"
   - Track progress with line ranges

**Response template**:
```
Added input: [Name]
- Source: [path/url]
- Type: [type]
- Size: [estimate]
- Status: Not processed

Updated: 01-INPUTS/INDEX.md

[If large input:]
Note: This is a large input ([N] lines). Will process in chunks with full attention.

Ready to add more inputs or use >>extract to process.
```

---

### `>>extract`

**Intent**: Process inputs and extract information

**Protocol**:

1. **Checkpoint consideration**: Before starting large extraction, assess context usage
   - If high, announce: "I'll set a checkpoint before proceeding with extraction."

2. **For each unprocessed input**:
   - Read content based on type
   - For large inputs: process methodically, chunk by chunk
   - Extract to categories:
     - Themes & Patterns (T1, T2...)
     - Requirements (R1, R2...)
     - Constraints (C1, C2...)
     - Stakeholders (S1, S2...)
     - Decisions Already Made (D1, D2...)
     - Contradictions & Ambiguities (A1, A2...)
   - Update INDEX.md status to "[x] Extracted"

3. **Create/update `02-EXTRACTIONS.md`**:
   - Source attribution table with IDs
   - Full extraction by category
   - Cross-references between items

4. **Surface questions to `08-OPEN-QUESTIONS.md`**:
   - Questions discovered during extraction
   - Full context for each question
   - Impact description

5. **Cross-reference check**: Ensure all sources are attributed

6. **Update `00-OVERVIEW.md`** status

7. **Present summary and questions to human**

**Response template**:
```
Extraction complete for [N] inputs.

Extracted:
- [N] themes identified (T1-TN)
- [N] requirements captured (R1-RN)
- [N] constraints noted (C1-CN)
- [N] decisions found (D1-DN)
- [N] ambiguities flagged (A1-AN)

Updated:
- 02-EXTRACTIONS.md
- 01-INPUTS/INDEX.md (statuses)
- 08-OPEN-QUESTIONS.md ([N] questions)

[If questions exist:]
There are [N] open questions in 08-OPEN-QUESTIONS.md.
Please review and add your responses, then use >>continue.

Ready for >>conceptualize when questions are resolved.
```

---

### `>>conceptualize`

**Intent**: Build concept from extractions

**Protocol**:

1. **Review `02-EXTRACTIONS.md`**

2. **Checkpoint consideration**: Assess context before deep work

3. **Structure concept**:
   - Identify main concept scope
   - Identify sub-concepts (max 7, or suggest splitting)
   - Define relationships and dependencies

4. **Create/update `03-CONCEPT.md`**:
   - Vision (2-3 sentences)
   - Scope (In/Out with rationale)
   - Sub-concepts table (with links)
   - Core concept sections with source references (R1, T2, etc.)
   - Non-technical aspects
   - Dependencies
   - Risks & Mitigations
   - Success Criteria
   - Traceability matrix

5. **Create sub-concept documents** as needed (max 7):
   - `03-CONCEPT-[name].md` for each
   - Link from main concept

6. **Cross-reference update**: Update all traceability links

7. **Proactive refinement check**: Flag any inconsistencies with extractions

8. **Present to human for feedback**

**Response template**:
```
Concept structure created.

Main Concept: [Name]
- Vision: [Brief]
- In Scope: [N] items
- Out of Scope: [N] items (with rationale)

Sub-Concepts: [N] (max 7)
1. [Name] - [Brief description]
2. [Name] - [Brief description]
...

Created/Updated:
- 03-CONCEPT.md
- 03-CONCEPT-[sub1].md
- 03-CONCEPT-[sub2].md

Traceability: All concept elements linked to source requirements/themes.

[If issues found:]
Note: Found [N] inconsistencies with extractions - see 08-OPEN-QUESTIONS.md

Ready for >>plan when concept is approved.
```

---

### `>>plan`

**Intent**: Generate work plan from concept

**Protocol**:

1. **Ask format first** (CRITICAL):
   ```
   What format would you like for the work plan?
   - `generic` - Flexible phases/work-packages/tasks
   - `jira` - Epics/Stories (with optional sub-tasks)
   - `github` - Issues with labels and milestones
   - `custom` - Describe your structure
   ```

2. **Wait for human response**

3. **Generate `04-WORKPLAN.md`** in chosen format:
   - Overview with totals
   - Traceability matrix linking to concept
   - Phases/Epics with work packages/stories
   - Tasks with types and dependencies
   - Progress summary

4. **Cross-reference update**: Link all items to concept elements

5. **Present for feedback**

**Response template**:
```
Work plan created in [format] format.

Overview:
- Phases/Epics: [N]
- Work Packages/Stories: [N]
- Tasks: [N]
- Complexity: [High/Medium/Low]

Structure:
Phase 1: [Name] - [N] work packages
Phase 2: [Name] - [N] work packages
...

Created: 04-WORKPLAN.md

All items traced to concept elements.

Ready for >>roadmap when plan is approved.
```

---

### `>>roadmap`

**Intent**: Generate roadmap with dependencies and visualization

**Protocol**:

1. **Analyze dependencies** from `04-WORKPLAN.md`
   - Identify critical path
   - Find parallel opportunities
   - Note bottlenecks

2. **Generate `05-ROADMAP.md`**:
   - Dependency analysis
   - Sequence waves (Foundation, Core, Integration, etc.)
   - Milestones
   - Risk points

3. **Generate `05-ROADMAP.mermaid.md`**:
   - Dependency graph (mermaid graph LR)
   - Timeline view if dates available (mermaid gantt)
   - Critical path highlight
   - Status overview (mermaid pie)

4. **Update `00-OVERVIEW.md`** status

5. **Present to human for review**

**Response template**:
```
Roadmap generated.

Dependency Analysis:
- Critical Path: [Brief description]
- Parallel Opportunities: [Brief description]

Waves:
- Wave 1 (Foundation): [N] work packages - can start immediately
- Wave 2 (Core): [N] work packages - after Wave 1
- Wave 3 (Integration): [N] work packages - after Wave 2
...

Milestones: [N] defined

Created:
- 05-ROADMAP.md
- 05-ROADMAP.mermaid.md (visual diagrams)

Ready for >>finalize when roadmap is approved, or >>refine [phase] for changes.
```

---

### `>>refine <phase>`

**Intent**: Enter refinement cycle at specified phase

**Syntax**: `>>refine extract` | `>>refine concept` | `>>refine plan` | `>>refine roadmap`

**Protocol**:

1. **Log in `07-REFINEMENT-LOG.md`**:
   ```markdown
   ## Refinement Cycle [N]
   **Date**: [date]
   **Entry Point**: [phase]
   **Trigger**: Human request | Agent detection
   **Version**: [current version]

   ### Changes Made
   [To be filled]

   ### Cross-Reference Updates
   - [ ] Updated traceability in [doc]
   - [ ] Updated source references in [doc]
   ```

2. **Apply changes to entry phase**

3. **Cascade forward** (CRITICAL):
   - `extract` → concept → plan → roadmap
   - `concept` → plan → roadmap
   - `plan` → roadmap
   - `roadmap` → only roadmap

4. **Update ALL cross-references** in affected documents

5. **Update `00-OVERVIEW.md`**

6. **Notify human of all cascading changes**

**Response template**:
```
Refinement cycle [N] started at [phase].

Changes made:
- [Phase]: [Changes]

Cascaded to:
- [Next phase]: [Changes]
- [Next phase]: [Changes]

Cross-references updated:
- [List of documents]

Updated: 07-REFINEMENT-LOG.md

Refinement complete. Ready to continue.
```

**Proactive Refinement Detection**:
Agent should suggest refinement when detecting:
- Inconsistencies between documents
- New information contradicting existing content
- Gaps in traceability
- Scope changes implied by recent inputs

---

### `>>finalize`

**Intent**: Complete concept work and promote to top-level folders

**Protocol**:

1. **Verify completeness**:
   - All inputs processed (check INDEX.md)
   - No unresolved questions in `08-OPEN-QUESTIONS.md`
   - Concept, workplan, and roadmap complete

2. **Determine version**:
   - Check if `ai-agent/concepts/[name]/` exists
   - If new: create `v1/`
   - If exists: create next version `vN/`

3. **Create finalized folders**:
   - `ai-agent/concepts/[name]/vN/`
   - `ai-agent/workplans/[name]/vN/`

4. **Copy finalized documents**:
   - Concept docs → `concepts/[name]/vN/`
   - Workplan + roadmap → `workplans/[name]/vN/`
   - Create `INPUTS-SUMMARY.md` in concept folder

5. **Update working folder** status to "Finalized"

6. **Ask human**: Archive or keep working folder?

**Response template**:
```
Verifying completeness...
✓ All inputs processed
✓ No unresolved questions
✓ Concept complete
✓ Work plan complete
✓ Roadmap complete

Finalizing...

Created:
- ai-agent/concepts/[name]/v1/
  - CONCEPT.md
  - CONCEPT-[sub].md (x[N])
  - INPUTS-SUMMARY.md
- ai-agent/workplans/[name]/v1/
  - WORKPLAN.md
  - ROADMAP.md
  - ROADMAP.mermaid.md

Updated: 00-OVERVIEW.md (status: Finalized)

Concept work complete! 🎉

Archive the working folder? (y/n)
```

---

### `>>new-version`

**Intent**: Create new version for major concept revision

**When to use**:
- Weeks have passed with significant changes
- New major inputs (meetings, discoveries)
- Fundamental direction change

**Protocol**:

1. **Create new work folder**: `NNN-concept-name-v2`

2. **Copy current state** as starting point

3. **Reference previous version** in `00-OVERVIEW.md`

4. **Fresh `07-REFINEMENT-LOG.md`** for new version

5. **Ready to process new inputs** through full workflow

**Response template**:
```
Creating new version for concept: [name]

Created: ai-agent/work/NNN-concept-name-v2/
- Copied current state as starting point
- Fresh refinement log
- Reference to v1 in overview

Ready to:
- >>add-input [new inputs]
- >>refine [phase] for updates
- >>continue with changes

What new inputs or changes should we process?
```

---

## Session Workflow

### Starting New Session (After Break)

When human says `>>continue`:

1. **Read knowledge base**:
   - `ai-agent/knowledge/SYSTEM-OVERVIEW.md` for project context
   - `ai-agent/knowledge/COMMANDS.md` for useful commands
2. **Read SSOT**: `00-OVERVIEW.md`
   - Work name and type
   - Overall status
   - Current phase
3. **Read Progress Log**: Last entry in `03-PROGRESS-LOG.md`
   - What was last completed
   - What's next
4. **Summarize**: 3-4 sentences max
5. **Confirm**: State next task specifically
6. **Wait**: For human approval

**Template**:
```
Work: [Name] (TYPE)
Status: [From SSOT]
Phase: [Current phase name]
Last: [Last completed item]
Next: [Specific task with file:line if applicable]

Ready to proceed?
```

### Continuing After Context Summary/Compression

When a session continues from a summarized context (e.g., after context window reset):

**Context Continuation Checklist** (CRITICAL - follow every time):
1. **Check git status** - Are there uncommitted changes?
2. **Re-read knowledge files**:
   - `ai-agent/knowledge/SYSTEM-OVERVIEW.md`
   - `ai-agent/knowledge/COMMANDS.md`
   - Relevant `subsystems/` docs mentioned in summary
3. **Re-read work SSOT**: `00-OVERVIEW.md`
4. **Read last progress log entry**: Check "Next Session Start Here"
5. **Verify "in progress" work**: Is there incomplete work mentioned?
6. **Ask if unclear**: "The summary mentions X - is this still the current state?"

**Proactive question**: After recovering context, ask:
```
I've recovered context from the summary. Should I update knowledge
with any insights from the previous session before continuing?
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
| 00-OVERVIEW.md | 2 pages | Refactor, archive old decisions |
| 01-REQUIREMENTS.md | 3 pages | Split feature or remove detail |
| 01-SCOPE.md | 2 pages | Be more concise |
| 02-IMPLEMENTATION-PLAN.md | 4 pages | Break phases into sub-features |
| 03-PROGRESS-LOG.md | Unlimited | Archive old entries (keep recent) |
| 04-TESTING-CHECKLIST.md | 2 pages | Remove duplicate scenarios |
| 05-ANALYSIS.md | 3 pages | Move reusable insights to knowledge |
| 06-PR-MESSAGE.md | 1 page | Keep summary concise |

### Extended Documents (05, 06)

**05-ANALYSIS.md** - Use when:
- Feature requires significant codebase research
- Analysis is specific to this work item (not reusable)
- You need to document investigation findings
- **Don't use for**: Insights that should go in knowledge docs

**06-PR-MESSAGE.md** - Use when:
- Work will result in a PR
- Work spans multiple sessions
- Maintaining PR context throughout is valuable
- **Update**: Throughout development, especially at `>>wrap`

### Append-Only Rule

`03-PROGRESS-LOG.md` is **append-only**:
- ✅ Add new entries at the end
- ❌ Never modify old entries (except typos)
- ❌ Never create separate session summary files
- ❌ Never duplicate info already in the log

### SSOT Updates

`00-OVERVIEW.md` should be updated only when:
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
1. **Ensure knowledge directory exists**:
   - If `ai-agent/knowledge/` doesn't exist, create it: `mkdir -p ai-agent/knowledge`

2. **Check for existing knowledge**:
   - Look for `ai-agent/knowledge/SYSTEM-OVERVIEW.md`
   - If exists: Read it and identify gaps
   - If doesn't exist: Note that full QnA is needed

3. **Prepare QnA questions**:
   - Review what human already provided
   - Generate questions for missing information:
     - Project purpose (if not clear)
     - Domain context (if not mentioned)
     - Tech stack details (if incomplete)
     - Architecture patterns (if not described)
     - Key conventions (if not documented)
     - Development workflow (if not explained)
     - Known gotchas (if not listed)

4. **Conduct QnA session**:
   - Present questions to human
   - Wait for answers
   - Clarify anything ambiguous

5. **Create/Update SYSTEM-OVERVIEW.md**:
   - Merge human-provided content + QnA answers
   - Fill template completely
   - Save to `ai-agent/knowledge/SYSTEM-OVERVIEW.md`

6. **Confirm completion**:
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
1. **Ensure knowledge directory exists**:
   - If `ai-agent/knowledge/` doesn't exist, create it: `mkdir -p ai-agent/knowledge`

2. **Scan directory structure**:
   - Map folders and key files
   - Identify entry points (main, server, CLI)
   - Find configuration files
   - Note build and test setup

3. **Create REPOSITORY-MAP.md**:
   - Document directory structure
   - List key files by category
   - Identify main workflows
   - Note file counts and technologies

4. **Analyze code patterns**:
   - Scan for data models/schemas
   - Find API endpoints/routes
   - Identify utilities and helpers
   - Note design patterns
   - Find authentication/authorization setup

5. **Create CONCEPTS-INDEX.md**:
   - Catalog discovered patterns
   - List data models with locations
   - Document API structure
   - Note common abstractions
   - Link to relevant files

6. **Confirm completion**:
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
- `00-OVERVIEW.md` - SSOT for features and bugs
- `01-REQUIREMENTS.md` - Requirements for features
- `02-IMPLEMENTATION-PLAN.md` - Implementation phases
- `03-PROGRESS-LOG.md` - Session log
- `04-TESTING-CHECKLIST.md` - Test scenarios
- `05-ANALYSIS.md` - Optional: feature-specific research
- `06-PR-MESSAGE.md` - Optional: PR draft

### Maintenance Templates
`meta/templates/maintenance/`:
- `00-OVERVIEW.md` - SSOT for maintenance work
- `01-SCOPE.md` - Scope and compatibility concerns
- `02-IMPLEMENTATION-PLAN.md` - Implementation phases
- `03-PROGRESS-LOG.md` - Session log
- `04-TESTING-CHECKLIST.md` - Test scenarios

### Concept Templates
`meta/templates/concept/`:
- `00-OVERVIEW.md` - SSOT for concept work
- `01-INPUTS-INDEX.md` - Input inventory (goes in `01-INPUTS/` folder)
- `02-EXTRACTIONS.md` - Extracted information with IDs
- `03-CONCEPT.md` - Main concept document
- `03-CONCEPT-SUBCONCEPT.md` - Sub-concept template
- `04-WORKPLAN.md` - Generic work plan format
- `04-WORKPLAN-JIRA.md` - Jira format work plan
- `05-ROADMAP.md` - Sequencing and dependencies
- `05-ROADMAP-MERMAID.md` - Mermaid visualization template
- `06-PROGRESS-LOG.md` - Session log for concepts
- `07-REFINEMENT-LOG.md` - Refinement cycle tracking
- `08-OPEN-QUESTIONS.md` - Questions awaiting human input

### Knowledge Templates
`meta/templates/knowledge/`:
- `SYSTEM-OVERVIEW.md` - High-level project information
- `REPOSITORY-MAP.md` - Auto-generated repository structure
- `CONCEPTS-INDEX.md` - Catalog of patterns and concepts
- `COMMANDS.md` - Project-specific commands
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

✅ Every session starts by reading SSOT from the work folder
✅ Work items are in numbered folders (001-TYPE-name)
✅ Progress log grows by appending (never recreating)
✅ Handoffs include specific next task with file path
✅ Documents stay within max length
✅ Human can resume work in < 2 minutes
✅ Core docs per work item (plus optional 05/06)
✅ Knowledge docs updated when valuable insights discovered
✅ Knowledge checkpoint done at >>wrap
✅ No duplicate summaries

---

## Quick Reference

| Human Says | You Do |
|-----------|--------|
| `>>init-knowledge` | Setup knowledge base: read existing overview, QnA for gaps, merge info |
| `>>scan-repo` | Scan codebase, generate REPOSITORY-MAP, CONCEPTS-INDEX, COMMANDS |
| `>>start [TYPE] X` | Check knowledge, create numbered work folder (NNN-TYPE-name), ask questions |
| `>>continue` | Check knowledge, read SSOT from work folder, confirm next task |
| `>>wrap` | Knowledge checkpoint, update plan + log, summarize session |
| `>>checkpoint` | Capture knowledge mid-session (use at ~70-80% context) |
| `>>status` | Show current progress (no changes) |
| `>>test` | Create test checklist |
| `>>bug X` | Log bug, check knowledge, investigate, update knowledge if needed |
| `>>archive` | Verify complete, create final summary |

**Concept Workflow Commands**:

| Human Says | You Do |
|-----------|--------|
| `>>start concept X` | Create concept work folder, setup inputs structure |
| `>>add-input [path]` | Add input source, update INDEX.md |
| `>>extract` | Process inputs, create extractions with IDs (T1, R1, etc.) |
| `>>conceptualize` | Build concept from extractions (max 7 sub-concepts) |
| `>>plan` | Ask format first, generate work plan |
| `>>roadmap` | Generate roadmap + Mermaid visualization |
| `>>refine [phase]` | Refinement cycle with cascade (extract→concept→plan→roadmap) |
| `>>finalize` | Promote to concepts/ and workplans/ folders |
| `>>new-version` | Create new version for major revision |

**Work Types**: `feat` (feature), `maint` (maintenance), `bug` (bug fix), `concept` (conceptualization)

**Always**: Check knowledge base first, read SSOT, be specific, confirm major changes, respect limits, update checkboxes, document valuable insights, do knowledge checkpoint at wrap.

**Never**: Skip knowledge lookup, create new summaries, duplicate info, exceed max lengths, skip handoffs, use wrong folder numbering, ignore discovered patterns.

**Concept-Specific**: Always ask format before >>plan, cascade changes through >>refine, update cross-references on every change, don't skip/summarize large inputs.

---

This is your complete protocol. Follow it precisely for consistent, efficient collaboration with humans.
