# Guide for Humans

## Quick Copy-Paste Messages

**First session** (copy & paste to agent):
```
Please read ai-agent/meta/FOR-AGENTS.md - this explains our workflow system.
```

**After context loss** (agent crashed/closed):
```
Please read ai-agent/meta/FOR-AGENTS.md to understand our workflow system, then >>continue
```

---

## TL;DR

Use **meta-instructions** (shortcuts starting with `>>`) to work with AI:

**Setup** (first time):
- `>>init-knowledge` - Set up project knowledge (you + AI QnA)
- `>>scan-repo` - Scan codebase and create maps

**Work** (regular work):
- `>>start [TYPE] name` - Start new work (feat/maint/bug/concept)
- `>>continue` - Resume work
- `>>wrap` - End session
- `>>checkpoint` - Capture knowledge mid-session
- `>>status` - Get current status
- `>>test` - Start testing phase

**Concept Work** (for complex planning):
- `>>start concept name` - Start concept work
- `>>add-input [path]` - Add input sources
- `>>extract` - Process inputs
- `>>conceptualize` - Build concept
- `>>plan` - Generate work plan
- `>>roadmap` - Generate roadmap
- `>>finalize` - Complete and promote

**Work Types**: `feat` (feature), `maint` (maintenance), `bug` (bug fix), `concept` (conceptualization)

That's it. AI handles the rest.

---

## Project Structure

The meta system organizes your work like this:

```
project-root/ai-agent/
├── meta/               ← System docs (you're reading these)
├── work/               ← Active work (features, maintenance, bugs, concepts)
│   ├── 001-feat-login/       ← Feature work
│   ├── 002-maint-deps/       ← Maintenance work
│   ├── 003-bug-auth-fix/     ← Bug fix work
│   └── 004-concept-platform/ ← Concept work (during creation)
├── concepts/           ← Finalized concepts (after >>finalize)
│   └── [name]/v1/
├── workplans/          ← Finalized work plans (after >>finalize)
│   └── [name]/v1/
└── knowledge/          ← Project knowledge base
    ├── SYSTEM-OVERVIEW.md
    ├── COMMANDS.md           ← Project-specific commands
    └── subsystems/
```

## Work Types

| Type | Prefix | Use For |
|------|--------|---------|
| Feature | `feat` | New functionality, enhancements |
| Maintenance | `maint` | Dependency updates, refactoring, security audits |
| Bug | `bug` | Bug fixes |
| Concept | `concept` | Complex conceptualization, work plans, roadmaps |

## The Document System

Each work item gets its own numbered folder. The core documents vary by type:

**Features (`feat`)** - Full documentation:
```
ai-agent/work/001-feat-user-auth/
├── 00-OVERVIEW.md             ← Single source of truth (SSOT)
├── 01-REQUIREMENTS.md         ← What we're building
├── 02-IMPLEMENTATION-PLAN.md  ← How we're building it
├── 03-PROGRESS-LOG.md         ← What we did (append-only)
├── 04-TESTING-CHECKLIST.md    ← Test scenarios
├── 05-ANALYSIS.md             ← Optional: feature research
└── 06-PR-MESSAGE.md           ← Optional: PR draft
```

**Maintenance (`maint`)** - Lighter documentation:
```
ai-agent/work/002-maint-deps-update/
├── 00-OVERVIEW.md             ← SSOT
├── 01-SCOPE.md                ← What's included, compatibility
├── 02-IMPLEMENTATION-PLAN.md  ← Implementation phases
├── 03-PROGRESS-LOG.md         ← Session log
└── 04-TESTING-CHECKLIST.md    ← Test scenarios
```

**Bugs (`bug`)** - Use feature templates with focus on reproduction and fix.

---

## Knowledge System

The knowledge system helps AI understand your project better and retain insights across features.

### What's in Knowledge?

```
ai-agent/knowledge/
├── SYSTEM-OVERVIEW.md      ← Project basics (you fill this or QnA with AI)
├── REPOSITORY-MAP.md       ← AI-generated: directory structure
├── CONCEPTS-INDEX.md       ← AI-generated: patterns, APIs, models
├── COMMANDS.md             ← Project-specific commands and gotchas
└── subsystems/
    └── [name].md          ← AI-maintained: deep dives into subsystems
```

### When to Use Knowledge

**Initial Setup** (optional but recommended):
1. Fill out `SYSTEM-OVERVIEW.md` with project basics
   - OR do a QnA session where AI asks about your project
2. AI can scan repository to generate `REPOSITORY-MAP.md`

**During Development**:
- AI automatically reads knowledge docs before starting features
- AI updates knowledge when discovering important patterns
- You don't need to manage this - AI handles it

**Benefits**:
- AI starts with context instead of scanning entire codebase
- Insights from one feature help with later features
- Subsystem knowledge accumulates over time

### How to Start

**Step 0 - First session only** (point agent to the system):
```
Please read ai-agent/meta/FOR-AGENTS.md - this explains our workflow system.
```

**After context loss** (agent window closed, crash, new session):
```
Please read ai-agent/meta/FOR-AGENTS.md to understand our workflow system, then >>continue
```

**Recommended: Combined approach** (best results):
```
Human: [Optionally fill out knowledge/SYSTEM-OVERVIEW.md with what you know]
Human: >>init-knowledge
AI: [Reads your overview, asks questions to fill gaps]
AI: [Creates complete SYSTEM-OVERVIEW.md]
Human: >>scan-repo
AI: [Scans codebase, creates maps]
```

**Quick start** (skip knowledge setup):
```
Human: >>start my-first-feature
[AI works without project knowledge, learns as it goes]
```

You can always add knowledge later!

---

### `>>scan-repo`

**What it does**: Scans your codebase and generates knowledge maps
**AI response**: Creates REPOSITORY-MAP and CONCEPTS-INDEX with discovered patterns

**Example**:
```
Human: >>scan-repo
AI: Scanning repository structure...

    Created: knowledge/REPOSITORY-MAP.md
    - 12 directories mapped
    - 3 entry points found
    - 5 main workflows documented

    Created: knowledge/CONCEPTS-INDEX.md
    - 8 data models cataloged
    - 15 API endpoints mapped
    - 4 patterns identified

    Key findings:
    - Architecture: Express.js REST API
    - Entry point: src/server.ts
    - Test framework: Jest

    Your knowledge base is ready! Use >>start [feature-name] to begin.
```

**Next**: Start your first feature with `>>start`

**Note**: This can use many tokens for large repos. AI focuses on high-value info.

---

### `>>start [TYPE] <name>`

**What it does**: Initializes new work (feature, maintenance, or bug)
**AI response**: Creates foundation documents, asks questions

**Syntax**:
- `>>start feat user-notifications` - New feature
- `>>start maint deps-update` - Maintenance work
- `>>start bug login-issue` - Bug fix
- `>>start my-feature` - Defaults to `feat` if type omitted

**Example**:
```
Human: >>start feat user-notifications
AI: I'll create the foundation for feat: user-notifications.

    Created work folder: ai-agent/work/001-feat-user-notifications/

    Created:
    - 00-OVERVIEW.md (draft)
    - 01-REQUIREMENTS.md (draft)

    Questions about requirements:
    1. What types of notifications? (email, in-app, push?)
    2. Real-time or batched?
    3. [...]
```

**Next**: Answer questions → AI creates plan → You approve → Implementation starts

---

### `>>continue`

**What it does**: Resumes work on current work item
**AI response**: Reads state, confirms next task

**Example**:
```
Human: >>continue
AI: Work: User Notifications (feat)
    Status: Phase 2 - Backend API (in progress)
    Last: Database models created
    Next: Implement NotificationService.send()

    Ready to continue?
```

**Next**: Say "yes" → AI continues work

---

### `>>wrap`

**What it does**: Ends current session with proper handoff
**AI response**: Updates docs, captures knowledge, logs progress, sets next task

**Example**:
```
Human: >>wrap
AI: Session summary:
    ✓ Completed: NotificationService.send()
    ✓ Completed: Email template rendering
    ✓ Tests: All passing
    ✓ Knowledge: Updated CONCEPTS-INDEX.md with notification patterns

    Updated: 03-PROGRESS-LOG.md with handoff

    Next session: Implement notification preferences UI
```

**Next**: Session ends, context preserved for next time

---

### `>>checkpoint`

**What it does**: Captures knowledge mid-session (use in long sessions)
**AI response**: Updates knowledge docs, preserves context

**When to use**:
- Long sessions approaching context limits
- You've made significant discoveries worth documenting
- Before expected context compression

**Example**:
```
Human: >>checkpoint
AI: Knowledge checkpoint captured.

    Updated:
    - CONCEPTS-INDEX.md: Added authentication flow pattern
    - COMMANDS.md: Added database migration commands

    Current context preserved for continuation.
    Ready to proceed.
```

**Note**: This does NOT end the session - work continues after checkpoint.

---

### `>>status`

**What it does**: Quick status check without changing anything
**AI response**: Current state summary

**Example**:
```
Human: >>status
AI: Feature: User Notifications
    Overall: 60% complete
    Current Phase: 2 of 4 (Backend API)
    Last update: 2025-11-28

    Completed phases:
    ✓ Phase 1: Database models

    In progress:
    ~ Phase 2: Backend API (75% done)

    Next:
    - Phase 3: Frontend UI
    - Phase 4: Testing
```

---

### `>>test`

**What it does**: Starts testing phase
**AI response**: Creates testing checklist

**Example**:
```
Human: >>test
AI: Creating 04-TESTING-CHECKLIST.md with test scenarios.

    Created 8 test scenarios:
    - Happy path tests (3)
    - Edge case tests (3)
    - Regression tests (2)

    Ready for you to test. Update checklist with results.
```

**Next**: Test each scenario, report results

---

### `>>bug <description>`

**What it does**: Reports a bug found during testing
**AI response**: Logs bug, asks for details, prepares fix

**Example**:
```
Human: >>bug Notification email not sent for in-app notifications
AI: Bug logged. Questions:
    1. Steps to reproduce?
    2. Expected vs actual behavior?
    3. Any error messages?

    I'll investigate NotificationService after your answers.
```

---

### `>>archive`

**What it does**: Feature complete, archive old documents
**AI response**: Creates final summary, moves docs to archive

**Example**:
```
Human: >>archive
AI: Verifying completion...
    ✓ All requirements met
    ✓ All tests passing

    Created: archive/2025-11-28-user-notifications-FINAL.md
    Moved to archive: [list of old docs]

    Kept in root: Core 5 documents (for reference)

    Feature complete! 🎉
```

---

## Concept Workflow

The concept workflow is for complex planning work that involves:
- Analyzing diverse inputs (conversations, documents, PDFs)
- Building structured concepts with sub-concepts
- Creating work plans and roadmaps
- Iterative refinement

### When to Use Concept Workflow

Use `>>start concept` when you need to:
- Process large amounts of raw input (meeting notes, conversations, requirements docs)
- Build a structured concept from messy inputs
- Create a work plan with phases and tasks
- Generate a roadmap with dependencies

**Don't use** for simple features - use `>>start feat` instead.

### Concept Workflow Overview

```
GATHER → EXTRACT → CONCEPTUALIZE → PLAN → ROADMAP → [REFINE] → FINALIZE
```

1. **Gather**: Add inputs (`>>add-input`)
2. **Extract**: Process inputs into structured data (`>>extract`)
3. **Conceptualize**: Build concept from extractions (`>>conceptualize`)
4. **Plan**: Generate work plan (`>>plan`)
5. **Roadmap**: Create dependency map (`>>roadmap`)
6. **Refine**: Iterate on any phase (`>>refine [phase]`)
7. **Finalize**: Promote to top-level folders (`>>finalize`)

### Concept Commands

#### `>>start concept <name>`
Starts a new concept work item.

```
Human: >>start concept new-platform-design
AI: Created work folder: ai-agent/work/001-concept-new-platform-design/

    Questions about inputs:
    1. What raw inputs will we analyze?
    2. Are there URLs to fetch or files to add?

    Use >>add-input [path/url] to add sources.
```

#### `>>add-input <path-or-url>`
Adds an input source for analysis.

```
Human: >>add-input ./conversations/planning-meeting.json
AI: Added input: planning-meeting.json
    - Type: conversation
    - Size: ~5000 lines
    - Status: Not processed

    Ready to add more or use >>extract.
```

**Note**: For large inputs (10000+ lines), AI processes everything - no summarization or skipping.

#### `>>extract`
Processes inputs and extracts structured information.

```
Human: >>extract
AI: Extraction complete.

    Extracted:
    - 12 themes (T1-T12)
    - 8 requirements (R1-R8)
    - 3 constraints (C1-C3)
    - 2 ambiguities (A1-A2)

    Open questions: 4 (see 08-OPEN-QUESTIONS.md)
    Please review and add your responses.
```

#### `>>conceptualize`
Builds concept structure from extractions.

```
Human: >>conceptualize
AI: Concept structure created.

    Main Concept: New Platform Design
    - 5 sub-concepts defined
    - All elements traced to sources

    Ready for >>plan when approved.
```

#### `>>plan`
Generates work plan (asks for format first).

```
Human: >>plan
AI: What format for the work plan?
    - generic (phases/work-packages/tasks)
    - jira (Epics/Stories)
    - github (Issues/Milestones)
    - custom

Human: jira
AI: Work plan created in Jira format.
    - 4 Epics
    - 18 Stories
    - All traced to concept elements
```

#### `>>roadmap`
Generates roadmap with Mermaid visualization.

```
Human: >>roadmap
AI: Roadmap generated.

    Waves:
    - Wave 1 (Foundation): 4 work packages
    - Wave 2 (Core): 6 work packages
    - Wave 3 (Integration): 4 work packages

    Created:
    - 05-ROADMAP.md
    - 05-ROADMAP.mermaid.md (visual diagrams)
```

#### `>>refine <phase>`
Enters refinement cycle at specified phase.

```
Human: >>refine concept
AI: Refinement cycle started at concept.

    What changes should I make?

Human: Add security as a sub-concept
AI: Changes made:
    - Concept: Added security sub-concept
    - Cascaded to: plan, roadmap
    - Cross-references updated
```

#### `>>finalize`
Completes concept work and promotes to top-level folders.

```
Human: >>finalize
AI: Verifying completeness...
    ✓ All inputs processed
    ✓ No open questions
    ✓ Concept complete

    Created:
    - ai-agent/concepts/new-platform-design/v1/
    - ai-agent/workplans/new-platform-design/v1/

    Concept work complete! 🎉
```

#### `>>new-version`
Creates new version for major revisions (weeks later, new inputs).

```
Human: >>new-version
AI: Creating new version for concept: new-platform-design

    Created: ai-agent/work/002-concept-new-platform-design-v2/
    Ready for new inputs and changes.
```

### Open Questions Workflow

During concept work, AI generates questions in `08-OPEN-QUESTIONS.md`:

1. AI adds questions with full context
2. You add answers in "Human Response" sections
3. Run `>>continue` for AI to process answers
4. Resolved questions move to archive

### Concept Document Structure

```
ai-agent/work/NNN-concept-name/
├── 00-OVERVIEW.md              ← SSOT for concept work
├── 01-INPUTS/
│   └── INDEX.md               ← Inventory of all inputs
├── 02-EXTRACTIONS.md          ← Structured data from inputs
├── 03-CONCEPT.md              ← Main concept
├── 03-CONCEPT-[sub].md        ← Sub-concepts (max 7)
├── 04-WORKPLAN.md             ← Work breakdown
├── 05-ROADMAP.md              ← Dependency analysis
├── 05-ROADMAP.mermaid.md      ← Visual diagrams
├── 06-PROGRESS-LOG.md         ← Session log
├── 07-REFINEMENT-LOG.md       ← Refinement tracking
└── 08-OPEN-QUESTIONS.md       ← Questions for human input
```

### Versioning

Finalized concepts support versions:

```
ai-agent/concepts/[name]/
├── v1/                         ← Original version
│   ├── CONCEPT.md
│   └── CONCEPT-[sub].md
└── v2/                         ← Major revision
    └── ...
```

Use `>>new-version` when:
- Weeks have passed with significant changes
- New major inputs (meetings, discoveries)
- Fundamental direction change

---

## Detailed Workflows

### Starting a New Feature

1. **You say**: `>>start my-feature`
2. **AI creates**: 00-FEATURE-OVERVIEW.md, 01-REQUIREMENTS.md (drafts)
3. **AI asks**: Clarifying questions
4. **You answer**: Questions
5. **AI creates**: 02-IMPLEMENTATION-PLAN.md
6. **You review**: Plan looks good?
7. **You say**: "Approved, start Phase 1"
8. **AI implements**: Phase by phase

**After each phase**:
- AI asks you to verify
- You test/review
- You say "looks good" or report issues
- AI moves to next phase

### Continuing After Break

1. **You say**: `>>continue`
2. **AI reads**: Knowledge base + SSOT + progress log
3. **AI summarizes**: Current state + next task
4. **You confirm**: "Yes" or adjust priority
5. **AI continues**: Work resumes

**No context loss**: AI knows exactly where you left off

### After Context Compression (Long Sessions)

When a session is very long and context gets summarized:

1. **AI automatically**: Re-reads knowledge files and work SSOT
2. **AI asks**: "Should I update knowledge with insights from the previous session?"
3. **You answer**: Yes/No, or provide guidance
4. **AI continues**: With recovered context

**Tip**: Use `>>checkpoint` proactively in long sessions to capture knowledge before compression happens.

### Ending a Session

1. **You say**: `>>wrap`
2. **AI updates**:
   - Marks completed items in plan
   - Appends session summary to progress log
   - Sets "Next Session Start Here"
3. **AI confirms**: What was done + what's next
4. **Done**: Session ends cleanly

### Testing a Feature

1. **You say**: `>>test`
2. **AI creates**: 04-TESTING-CHECKLIST.md
3. **You test**: Each scenario
4. **You report**:
   - `>>bug` for failures
   - Or update checklist directly
5. **AI fixes**: Issues you found
6. **Repeat**: Until all tests pass

### Completing a Feature

1. **Verify**: All tests pass
2. **You say**: `>>archive`
3. **AI verifies**: Requirements met, tests pass
4. **AI creates**: Final summary in archive/
5. **AI moves**: Old docs to archive/
6. **Done**: Feature complete, docs clean

---

## Best Practices

### Do ✅

1. **Use meta-instructions**: `>>continue` instead of "continue where we left off"
2. **Test after each phase**: Catch issues early
3. **Give specific feedback**: "Bug in file.ts:123 - when X, Y happens"
4. **Archive when done**: Keep `/ai-agent/features/` clean
5. **Read SSOT when confused**: All current info is there

### Don't ❌

1. **Don't be vague**: "something's wrong" → AI can't help
2. **Don't skip testing**: Test after each phase, not at end
3. **Don't let files pile up**: Use `>>archive` when done
4. **Don't ignore blockers**: Tell AI what's blocking you
5. **Don't assume context**: AI needs to re-read SSOT each session

---

## Document Guidelines

### Core Documents

**00-OVERVIEW.md** (max 2 pages)
- Quick scan of entire work item
- Current status
- Key decisions
- Links to other docs

**01-REQUIREMENTS.md** (max 3 pages) - for features/bugs
- What needs to be built
- Acceptance criteria (checkboxes)
- Edge cases
- Out of scope (explicit)

**01-SCOPE.md** (max 2 pages) - for maintenance
- What's included
- Compatibility concerns
- Success criteria

**02-IMPLEMENTATION-PLAN.md** (max 4 pages)
- Phases (numbered)
- For each phase: objective, files, changes, status
- Dependencies between phases

**03-PROGRESS-LOG.md** (unlimited, but archive old entries)
- Date + session number
- What was completed
- Issues found/resolved
- Knowledge updated
- Next session start point

**04-TESTING-CHECKLIST.md** (max 2 pages)
- Test scenarios
- Steps to reproduce
- Expected result
- Status: Not Tested | Pass | Fail

### Optional Documents (Features)

**05-ANALYSIS.md** (max 3 pages)
- Feature-specific research
- Codebase exploration findings
- Technical decisions
- Use when: Feature requires significant investigation

**06-PR-MESSAGE.md** (max 1 page)
- PR title and summary
- Changes list
- Testing notes
- Use when: Work spans multiple sessions, helps maintain PR context

**If exceeds max**: Refactor or archive

---

## Troubleshooting

### "Too many files in /ai-agent/work/"
→ Use `>>archive` to clean up completed work

### "Don't know what to work on next"
→ Use `>>status` or check progress log "Next Session Start Here"

### "AI seems confused"
→ Say `>>continue` (forces AI to re-read SSOT)

### "Tests keep failing"
→ Use `>>bug` for each failure, be specific with reproduction steps

### "Work seems stuck"
→ Check 00-OVERVIEW.md for blockers, discuss with AI

### "Long session, worried about losing context"
→ Use `>>checkpoint` to capture knowledge before context compression

---

## Examples

### Example 1: Quick Feature

```
Human: >>start add-export-button
AI: [Creates docs, asks questions]
Human: [Answers]
AI: [Creates plan]
Human: Approved
AI: [Implements Phase 1]
AI: Phase 1 complete, verify?
Human: Works, continue
AI: [Implements Phase 2]
Human: >>test
AI: [Creates test checklist]
Human: All tests pass
Human: >>archive
AI: Feature complete! 🎉
```

**Duration**: 2-3 sessions

### Example 2: Complex Feature with Issues

```
Human: >>start user-authentication
AI: [Creates docs, asks questions]
Human: [Answers]
AI: [Creates multi-phase plan]
Human: Approved
AI: [Implements Phase 1-2]
Human: >>test
AI: [Creates checklist]
Human: >>bug Login fails for OAuth users
AI: [Investigates, fixes]
Human: Retest - still fails
AI: [More investigation, different fix]
Human: Works now, continue
AI: [Implements Phase 3-4]
Human: >>wrap
[Next session]
Human: >>continue
AI: [Resumes Phase 4]
Human: >>test
AI: All tests pass
Human: >>archive
AI: Feature complete! 🎉
```

**Duration**: 5-6 sessions with debugging

---

## Advanced Tips

### Custom Meta-Instructions

You can create your own shortcuts:

**Example**: `>>deploy` could mean:
- Run all tests
- Create deployment checklist
- Verify production config

**How**: Just use it consistently, AI will learn the pattern

### Combining Meta-Instructions

```
>>continue and >>status
```
→ Resume work + show status

### Conditional Meta-Instructions

```
>>continue if tests pass, else >>bug
```
→ AI checks test status first

---

## Success Metrics

Your work is well-managed if:

- ✅ `>>continue` gets you working in < 2 minutes
- ✅ All docs fit on screen (respect max lengths)
- ✅ Status is always current in SSOT
- ✅ Progress log shows clear progression
- ✅ Knowledge gets updated when valuable insights discovered
- ✅ Long sessions use `>>checkpoint` to preserve context

---

## Getting Help

**Confused about meta-instruction?**
→ Check this file's reference section

**Confused about document structure?**
→ Look at templates in `meta/templates/features/` and `meta/templates/knowledge/`

**Confused about agent behavior?**
→ Check `FOR-AGENTS.md` to see what AI sees

**Want to understand the knowledge system?**
→ Check `meta/templates/knowledge/` for template examples

**Still confused?**
→ Just ask AI: "How does the meta system work?"

---

