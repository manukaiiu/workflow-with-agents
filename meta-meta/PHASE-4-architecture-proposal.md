# Phase 4: Hierarchical Workflow Architecture

**Status**: Proposal
**Created**: 2025-12-15
**Purpose**: Solve the context window bloat problem while implementing all feedback improvements

---

## Problem Statement

The workflow system has grown to 1700+ lines in FOR-AGENTS.md alone. This creates:

1. **Context consumption**: Reading the full system eats significant context window
2. **Retention failure**: Long documents get summarized/dropped, losing protocol details
3. **All-or-nothing**: Agent must read everything even when only doing one thing
4. **Growth ceiling**: Can't add new features without making the problem worse

The feedback from AID-CC project (FB-001 through FB-009) would add hundreds more lines if implemented in the current structure.

---

## Proposed Solution: Hierarchical Protocol Architecture

### Core Principle

**Load what you need, when you need it.**

Instead of one monolithic document, create a layered system where:
- Layer 1 (CORE) is always read (~150-200 lines)
- Layer 2 (PROTOCOLS) is read on-demand per command/situation
- Layer 3 (REFERENCE) is consulted only when specific questions arise

### Visual Architecture

```
ai-agent/meta/
├── CORE.md                    ← Always read (compact mental model)
│
├── protocols/                 ← Read on-demand per command
│   ├── start.md              ← >>start details
│   ├── continue.md           ← >>continue details
│   ├── wrap.md               ← >>wrap details
│   ├── checkpoint.md         ← >>checkpoint details
│   ├── pause.md              ← >>pause details (NEW from FB-009)
│   │
│   ├── concept/              ← Concept workflow (split for size)
│   │   ├── overview.md       ← Concept work mental model
│   │   ├── gather.md         ← >>start concept, >>add-input
│   │   ├── extract.md        ← >>extract
│   │   ├── conceptualize.md  ← >>conceptualize
│   │   ├── plan.md           ← >>plan
│   │   ├── roadmap.md        ← >>roadmap
│   │   ├── refine.md         ← >>refine
│   │   └── finalize.md       ← >>finalize
│   │
│   ├── feature.md            ← Feature workflow
│   ├── maintenance.md        ← Maintenance workflow
│   ├── bug.md                ← Bug workflow
│   │
│   └── recovery.md           ← Context loss recovery (FB-005)
│
├── reference/                 ← Consult when needed
│   ├── GLOSSARY.md           ← Extraction IDs, status codes (FB-001)
│   ├── ABBREVIATIONS.md      ← Domain terms pattern (FB-002)
│   ├── FILE-CONVENTIONS.md   ← Numbering, organization (FB-008)
│   ├── WORK-TYPES.md         ← Detailed type comparison
│   └── MODES.md              ← Technical vs Process modes (FB-006)
│
├── templates/                 ← Unchanged (existing templates)
│   ├── features/
│   ├── maintenance/
│   ├── concept/
│   └── knowledge/
│
├── FOR-HUMANS.md             ← Human guide (can stay as-is, less critical)
└── README.md                 ← Overview (can stay as-is)
```

---

## Layer 1: CORE.md

**Size target**: 150-200 lines
**When read**: Every session, always
**Purpose**: Mental model + navigation

### Proposed Structure

```markdown
# Workflow System Core

## Mental Model

You're working with a structured documentation system for human-AI collaboration.
Work happens in numbered folders. Documents track state. Commands trigger protocols.

## Work Types (Brief)

| Type | Prefix | When to Use |
|------|--------|-------------|
| feature | feat | Building new functionality |
| maintenance | maint | Updates, refactoring, audits |
| bug | bug | Fixing defects |
| concept | concept | Complex planning, analysis, roadmaps |

## Commands (Navigation)

When you see these commands, read the linked protocol:

| Command | Protocol File | Purpose |
|---------|---------------|---------|
| >>start [type] name | protocols/start.md | Begin new work |
| >>continue | protocols/continue.md | Resume work |
| >>wrap | protocols/wrap.md | End session |
| >>checkpoint | protocols/checkpoint.md | Mid-session save |
| >>pause | protocols/pause.md | Interrupt work |
| >>status | (inline below) | Quick status check |

**Concept-specific** (read protocols/concept/overview.md first):
| >>add-input | >>extract | >>conceptualize | >>plan | >>roadmap | >>refine | >>finalize |

## Session Start Protocol

Every session, do this:

1. Check: Is there active work? → `ls ai-agent/work/`
2. If yes: Read that work item's `00-OVERVIEW.md`
3. The OVERVIEW tells you:
   - Current phase and status
   - What to do next
   - Which protocol file to read if needed

## Context Recovery (After Summarization)

If your context was summarized/compressed:

1. Check git status (uncommitted changes?)
2. Read `ai-agent/work/[active]/00-OVERVIEW.md`
3. Read last entry in progress log
4. If OVERVIEW has "Pause Context" section, follow its resume steps
5. Confirm understanding with human before proceeding

## Quick Reference

**Status codes**: [ ] pending, [~] in progress, [x] complete, [P] paused
**Extraction IDs**: T=Theme, R=Requirement, C=Constraint, S=Stakeholder, D=Decision, A=Ambiguity
**File numbers**: 00-09 reserved for templates, 90+ for outputs

## Core Principles

1. **SSOT**: 00-OVERVIEW.md is truth for each work item
2. **Append-only**: Progress logs grow, never rewrite
3. **Self-sufficient**: Work items contain their own context
4. **On-demand**: Read protocol files only when executing that command
5. **Checkpoint often**: Capture knowledge before context loss

## I Need More Detail On...

- Starting work → `protocols/start.md`
- Continuing work → `protocols/continue.md`
- Concept workflow → `protocols/concept/overview.md`
- File naming conventions → `reference/FILE-CONVENTIONS.md`
- Extraction ID meanings → `reference/GLOSSARY.md`
- Work type differences → `reference/WORK-TYPES.md`
```

---

## Layer 2: Protocol Files

Each protocol file contains the detailed steps for one command or workflow phase.

### Design Principles for Protocol Files

1. **Self-contained**: Include all needed info, don't require reading other protocols
2. **Actionable**: Steps are numbered and concrete
3. **Navigable**: End with "Related Protocols" links
4. **Sized right**: 100-200 lines each (concept phases ~80-120 lines)

### Example: protocols/continue.md

```markdown
# Protocol: >>continue

**Trigger**: Human says `>>continue` or "resume", "keep going", "continue"
**Purpose**: Resume work on existing work item

## Protocol Steps

1. **Find active work**
   ```
   ls ai-agent/work/
   ```
   - If multiple folders, check which has status "In Progress" or "Paused"
   - If unclear, ask human which work item

2. **Read work SSOT**
   - Open `00-OVERVIEW.md` in the work folder
   - Note: work type, current phase, status

3. **Check for pause context**
   - If "Pause Context" section exists, follow its "To resume" steps
   - Remove or archive the pause context after resuming

4. **Read progress log**
   - Open `03-PROGRESS-LOG.md` (or `06-PROGRESS-LOG.md` for concepts)
   - Find "Next Session Start Here" in last entry

5. **Summarize to human** (max 4 sentences)
   ```
   Work: [Name] ([type])
   Status: [status]
   Phase: [current phase]
   Next: [specific task from progress log]

   Ready to proceed?
   ```

6. **Wait for confirmation** before starting work

## Do NOT

- Start working without confirming with human
- Re-read entire codebase (focus on specific files)
- Create new summary documents
- Assume anything from previous session (always re-read SSOT)

## Natural Language Triggers

These phrases should be treated as `>>continue`:
- "resume", "keep going", "continue where we left off"
- "pick up where we stopped", "let's continue"

## Related Protocols

- Work was paused? → Check for Pause Context in OVERVIEW
- Need to pause now? → `protocols/pause.md`
- Ending this session? → `protocols/wrap.md`
- Context feels stale? → `protocols/recovery.md`
```

### Example: protocols/pause.md (NEW - from FB-009)

```markdown
# Protocol: >>pause

**Trigger**: Human says `>>pause [reason]` or "let's stop here", "need to interrupt"
**Purpose**: Pause work item with context for easy resumption

## Protocol Steps

1. **Update status in 00-OVERVIEW.md**
   ```markdown
   **Status**: PAUSED - [reason]
   **Paused**: [YYYY-MM-DD]
   ```

2. **Add Pause Context section to 00-OVERVIEW.md**
   ```markdown
   ## Pause Context

   **Paused on**: [date]
   **Reason**: [why - user request, blocker, priority shift]
   **Resume with**: `>>continue` or read this OVERVIEW

   **State at pause**:
   - [What's done]
   - [What's in progress]
   - [Blockers or pending questions]

   **To resume**:
   1. [First specific step]
   2. [Second step]
   3. [etc.]
   ```

3. **Update progress log**
   - Add entry noting the pause
   - Include reason and resume instructions

4. **Confirm to human**
   ```
   Work item paused.

   To resume later: >>continue
   The OVERVIEW contains full context for resumption.
   ```

## When to Pause vs Other Actions

| Situation | Action |
|-----------|--------|
| Stopping for the day, work incomplete | >>pause |
| Work complete, ending session | >>wrap |
| Switching to different work item | >>pause current, then >>continue other |
| Waiting for human review | Status: "Awaiting Review" (not paused) |

## Related Protocols

- Resuming paused work → `protocols/continue.md`
- Ending session normally → `protocols/wrap.md`
```

---

## Layer 3: Reference Files

Reference files contain stable information that doesn't change per-session.

### reference/GLOSSARY.md (FB-001, FB-002)

```markdown
# Workflow Glossary

## Extraction IDs

Used in concept work extractions (02-EXTRACTIONS.md):

| ID | Category | Description |
|----|----------|-------------|
| T | Theme | Recurring patterns or concepts across inputs |
| R | Requirement | Specific requirements that must be met |
| C | Constraint | Limitations or boundaries |
| S | Stakeholder | People/groups with interest in outcome |
| D | Decision | Choices already made |
| A | Ambiguity | Contradictions or unclear areas |
| Q | Question | Open questions requiring input |

Example: `T1`, `R3`, `C2-A` (Constraint 2, variant A)

## Status Indicators

| Symbol | Meaning |
|--------|---------|
| [ ] | Not started / Pending |
| [~] | In progress |
| [x] | Complete |
| [P] | Paused |

## Priority Levels

| Code | Meaning |
|------|---------|
| H | High priority |
| M | Medium priority |
| L | Low priority |

## Work Type Prefixes

| Prefix | Full Name | Use For |
|--------|-----------|---------|
| feat | Feature | New functionality |
| maint | Maintenance | Updates, refactoring |
| bug | Bug | Defect fixes |
| concept | Concept | Planning, analysis |

## File Number Reservations

| Range | Purpose |
|-------|---------|
| 00-09 | Template/core documents |
| 10-89 | Work-item specific (if needed) |
| 90-99 | Outputs, deliverables |

## Domain Abbreviations Pattern

When using domain-specific abbreviations:
1. **Expand on first use**: "Healthcare Professional (HCP)"
2. **Add to work item glossary**: If document has many terms, add a Glossary section
3. **Common domains**: Create `ai-agent/knowledge/DOMAIN-GLOSSARY.md` for project
```

### reference/MODES.md (FB-006)

```markdown
# Concept Work Modes

Concept work operates in one of two modes:

## Technical Mode (Default)

**Use for**: System concepts, architecture, technical planning

**Characteristics**:
- Full extraction with IDs (T1, R1, C1...)
- Work plan with epics, stories, story points
- Technical roadmap with dependency analysis
- Mermaid visualizations

**Signal in OVERVIEW**: `**Mode**: Technical` (or omit - it's default)

## Process Mode

**Use for**: Process design, management work, templates, strategies

**Characteristics**:
- Lighter extraction (goals, considerations - no IDs needed)
- Deliverables folder instead of detailed work plan
- Dependency tracking instead of technical roadmap
- Output-focused

**Signal in OVERVIEW**: `**Mode**: Process`

## Choosing a Mode

| If outputs are... | Use Mode |
|-------------------|----------|
| Architecture specs, JIRA stories, technical designs | Technical |
| Templates, processes, strategies, guidelines | Process |
| Unclear | Start with Process, switch if complexity warrants |

## Mode Affects Which Files Are Created

| Document | Technical | Process |
|----------|-----------|---------|
| 00-OVERVIEW.md | Required | Required |
| 01-INPUTS/ | Required | Required |
| 02-EXTRACTIONS.md | Full with IDs | Light or skip |
| 03-CONCEPT.md | Full | Lighter |
| 04-WORKPLAN.md | Full | Optional |
| 05-ROADMAP.md | Full | Optional |
| 90-OUTPUTS/ | Optional | Primary focus |
```

---

## Self-Sufficient Work Items

A key part of this architecture: **work items should contain their own context**.

### Enhanced 00-OVERVIEW.md Template

```markdown
# [Work Type]: [Name]

**Status**: [Planning | In Progress | Paused | Awaiting Review | Complete]
**Type**: [feat | maint | bug | concept]
**Mode**: [Technical | Process] (concept only)
**Created**: [date]
**Last Updated**: [date]

---

## Quick Context (for agent recovery)

**Current Phase**: [e.g., Phase 2: Implementation]
**Last Action**: [What was just completed]
**Next Action**: [Specific next step]
**Protocol**: [Which protocol file applies, e.g., protocols/concept/plan.md]

---

## Summary

[2-3 sentences: what this work item is about]

---

## File Index

| File | Type | Purpose |
|------|------|---------|
| 00-OVERVIEW.md | Core | This file - status and navigation |
| 01-... | Core | ... |
| 90-OUTPUTS/ | Outputs | Deliverables |

---

## Decision Log

| Date | Topic | Decision | Rationale |
|------|-------|----------|-----------|
| | | | |

---

## Pause Context (if paused)

**Paused on**: [date]
**Reason**: [reason]
**To resume**:
1. [step]
2. [step]

---

## Human Action Items (if any)

Items requiring human-to-human discussion:
- [ ] [Item for meeting X]
- [ ] [Item for meeting Y]
```

---

## Migration Path

How to get from current state to new architecture:

### Phase 1: Create Structure
1. Create `protocols/` folder
2. Create `reference/` folder
3. Create CORE.md (extract from FOR-AGENTS.md)

### Phase 2: Extract Protocols
1. Move `>>start` content → `protocols/start.md`
2. Move `>>continue` content → `protocols/continue.md`
3. Move `>>wrap` content → `protocols/wrap.md`
4. Move concept workflow → `protocols/concept/*.md`
5. Move other commands → respective protocol files

### Phase 3: Create Reference Files
1. Create `reference/GLOSSARY.md` (FB-001, FB-002)
2. Create `reference/MODES.md` (FB-006)
3. Create `reference/FILE-CONVENTIONS.md` (FB-008)

### Phase 4: Implement New Features
1. Add `protocols/pause.md` (FB-009)
2. Add `protocols/recovery.md` (FB-005)
3. Add dialogue/feedback conventions (FB-007)
4. Add discussion items pattern (FB-004)

### Phase 5: Update Templates
1. Enhance 00-OVERVIEW.md with Quick Context section
2. Add Decision Log section
3. Add File Index section
4. Add Pause Context placeholder

### Phase 6: Deprecate Old Files
1. Keep FOR-AGENTS.md temporarily with redirect notice
2. Update FOR-HUMANS.md to reference new structure
3. Eventually archive FOR-AGENTS.md

---

## Size Estimates

| Component | Lines | When Read |
|-----------|-------|-----------|
| CORE.md | ~150-200 | Every session |
| protocols/start.md | ~100 | On >>start |
| protocols/continue.md | ~80 | On >>continue |
| protocols/wrap.md | ~80 | On >>wrap |
| protocols/concept/overview.md | ~100 | Starting concept work |
| protocols/concept/[phase].md | ~80 each | Per phase |
| reference/GLOSSARY.md | ~80 | When confused about IDs |
| reference/MODES.md | ~60 | When starting concept |

**Typical session context load**:
- Always: CORE.md (~150 lines)
- Plus one or two protocols (~150-200 lines)
- **Total: ~300-350 lines** vs current 1700+ lines

**Savings: ~80% reduction in mandatory reading**

---

## Addressing Each Feedback Item

| Feedback | How Addressed |
|----------|---------------|
| FB-001 (Extraction IDs) | reference/GLOSSARY.md |
| FB-002 (Domain abbreviations) | reference/GLOSSARY.md + pattern |
| FB-003 (Concept vs Knowledge) | CORE.md work types + reference/WORK-TYPES.md |
| FB-004 (Discussion items) | Template enhancement + reference |
| FB-005 (Context loss) | protocols/recovery.md + CORE.md recovery section |
| FB-006 (Process mode) | reference/MODES.md |
| FB-007 (Human-agent dialogue) | Template Decision Log + reference |
| FB-008 (File organization) | reference/FILE-CONVENTIONS.md |
| FB-009 (Pause/resume) | protocols/pause.md + CORE.md |

---

## Open Questions

1. **FOR-HUMANS.md**: Should it also be restructured, or is it fine as-is since humans can scroll?

2. **Protocol file format**: Should protocols be markdown or could they be structured data (YAML frontmatter + markdown body) for potential tooling?

3. **Versioning**: Should protocol files be versioned, or rely on git history?

4. **Discovery**: How does an agent learn about new protocols added later? (Answer: CORE.md command table is the registry)

5. **Nesting depth**: Is `protocols/concept/[phase].md` too deep, or is the organization worth it?

---

## Success Criteria

The new architecture succeeds if:

- [ ] Agent can start working after reading only CORE.md (~150 lines)
- [ ] Context recovery works reliably after summarization
- [ ] New features can be added without bloating mandatory reading
- [ ] Work items are self-sufficient for resumption
- [ ] All FB-001 through FB-009 feedback is addressed
- [ ] Total mandatory reading is <300 lines per session

---

## Next Steps (if approved)

1. Review and refine this proposal based on your feedback
2. Create the new folder structure
3. Write CORE.md
4. Migrate existing content to protocol files
5. Create reference files
6. Update templates
7. Test with a real work item
8. Deprecate FOR-AGENTS.md

---

**Feedback requested on**:
- Overall architecture approach
- CORE.md content and size
- Protocol file granularity (especially concept workflow split)
- Any missing considerations
