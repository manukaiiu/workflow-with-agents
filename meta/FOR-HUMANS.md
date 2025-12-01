# Guide for Humans

## TL;DR

Use **meta-instructions** (shortcuts starting with `>>`) to work with AI:

**Setup** (first time):
- `>>init-knowledge` - Set up project knowledge (you + AI QnA)
- `>>scan-repo` - Scan codebase and create maps

**Features** (regular work):
- `>>start feature-name` - Start new feature
- `>>continue` - Resume work
- `>>wrap` - End session
- `>>status` - Get current status
- `>>test` - Start testing phase

That's it. AI handles the rest.

---

## Project Structure

The meta system organizes your work like this:

```
project-root/ai-agent/
├── meta/               ← System docs (you're reading these)
├── features/           ← Your feature work goes here
│   ├── 001_login/      ← Each feature has its own folder
│   ├── 002_dashboard/
│   └── 003_reports/
└── knowledge/          ← Project knowledge base
    ├── SYSTEM-OVERVIEW.md
    └── subsystems/
```

## The 5-Document System (Per Feature)

Each feature gets its own numbered folder with **5 core documents**:

```
ai-agent/features/001_feature-name/
├── 00-FEATURE-OVERVIEW.md     ← Single source of truth (SSOT)
├── 01-REQUIREMENTS.md         ← What we're building
├── 02-IMPLEMENTATION-PLAN.md  ← How we're building it
├── 03-PROGRESS-LOG.md         ← What we did (append-only)
└── 04-TESTING-CHECKLIST.md    ← Test scenarios
```

**Rule**: Everything about a feature is in these 5 files. No more, no less.

---

## Knowledge System

The knowledge system helps AI understand your project better and retain insights across features.

### What's in Knowledge?

```
ai-agent/knowledge/
├── SYSTEM-OVERVIEW.md      ← Project basics (you fill this or QnA with AI)
├── REPOSITORY-MAP.md       ← AI-generated: directory structure
├── CONCEPTS-INDEX.md       ← AI-generated: patterns, APIs, models
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

### `>>start <feature-name>`

**What it does**: Initializes a new feature
**AI response**: Creates foundation documents, asks questions

**Example**:
```
Human: >>start user-notifications
AI: I'll create the foundation for user-notifications.

    Created feature folder: ai-agent/features/001_user-notifications/

    Created:
    - 00-FEATURE-OVERVIEW.md (draft)
    - 01-REQUIREMENTS.md (draft)

    Questions about requirements:
    1. What types of notifications? (email, in-app, push?)
    2. Real-time or batched?
    3. [...]
```

**Next**: Answer questions → AI creates plan → You approve → Implementation starts

---

### `>>continue`

**What it does**: Resumes work on current feature
**AI response**: Reads state, confirms next task

**Example**:
```
Human: >>continue
AI: Feature: User Notifications
    Status: Phase 2 - Backend API (in progress)
    Last: Database models created
    Next: Implement NotificationService.send()

    Ready to continue?
```

**Next**: Say "yes" → AI continues work

---

### `>>wrap`

**What it does**: Ends current session with proper handoff
**AI response**: Updates docs, logs progress, sets next task

**Example**:
```
Human: >>wrap
AI: Session summary:
    ✓ Completed: NotificationService.send()
    ✓ Completed: Email template rendering
    ✓ Tests: All passing

    Updated: 03-PROGRESS-LOG.md with handoff

    Next session: Implement notification preferences UI
```

**Next**: Session ends, context preserved for next time

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
2. **AI reads**: SSOT + progress log
3. **AI summarizes**: Current state + next task
4. **You confirm**: "Yes" or adjust priority
5. **AI continues**: Work resumes

**No context loss**: AI knows exactly where you left off

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

### For Each Core Document

**00-FEATURE-OVERVIEW.md** (max 2 pages)
- Quick scan of entire feature
- Current status
- Key decisions
- Links to other docs

**01-REQUIREMENTS.md** (max 3 pages)
- What needs to be built
- Acceptance criteria (checkboxes)
- Edge cases
- Out of scope (explicit)

**02-IMPLEMENTATION-PLAN.md** (max 4 pages)
- Phases (numbered)
- For each phase: objective, files, changes, status
- Dependencies between phases

**03-PROGRESS-LOG.md** (unlimited, but archive old entries)
- Date + session number
- What was completed
- Issues found/resolved
- Next session start point

**04-TESTING-CHECKLIST.md** (max 2 pages)
- Test scenarios
- Steps to reproduce
- Expected result
- Status: Not Tested | Pass | Fail

**If exceeds max**: Refactor or archive

---

## Troubleshooting

### "Too many files in /ai-agent/features/"
→ Use `>>archive` to clean up

### "Don't know what to work on next"
→ Use `>>status` or check progress log "Next Session Start Here"

### "AI seems confused"
→ Say `>>continue` (forces AI to re-read SSOT)

### "Tests keep failing"
→ Use `>>bug` for each failure, be specific with reproduction steps

### "Feature seems stuck"
→ Check 00-FEATURE-OVERVIEW.md for blockers, discuss with AI

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

Your feature is well-managed if:

- ✅ `>>continue` gets you working in < 2 minutes
- ✅ All docs fit on screen (respect max lengths)
- ✅ Status is always current in SSOT
- ✅ Progress log shows clear progression
- ✅ Only 5 core docs + archive in feature folder

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

