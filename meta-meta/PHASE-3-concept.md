# Phase 3: Concept Workflow - Design Document

**Status**: Implemented
**Created**: 2025-12-09
**Last Updated**: 2025-12-09
**Author**: AI Agent + Human collaboration

---

## Executive Summary

This document defines a new work type `concept` for the workflow system, designed to handle complex conceptualization work that involves:
- Analyzing diverse raw inputs (conversations, documents, PDFs) - including very large inputs
- Extracting and structuring information with high attention to detail
- Building multi-layered concepts with sub-concepts (max 7 before splitting)
- Creating work plans (phases, epics, work packages, tasks) in various formats
- Generating roadmaps with sequencing, parallelization, and Mermaid visualization
- Supporting iterative refinement cycles with version tracking

Unlike `feat`, `maint`, and `bug` work types which focus on implementation, `concept` focuses on **thinking, structuring, and planning** before implementation begins.

### Key Design Decisions (from feedback)
- **Flexible document lengths** - Limits are guidelines, not hard rules
- **Intelligent command matching** - Agent detects intent even without explicit `>>` commands
- **Two-phase structure** - Working folder during creation, promotion to top-level when finalized
- **Versioning support** - Major iterations get version folders
- **Proactive checkpoints** - Agent decides when to checkpoint, not just human
- **Large input handling** - Full processing of massive conversations (10000+ lines)
- **Open Questions workflow** - Dedicated sections for human answers

---

## Folder Architecture

### The Two-Phase Approach

Concept work has a unique lifecycle: it starts as active work, then the outputs become foundational project artifacts.

```
PHASE A: Active Work (Creation)          PHASE B: Finalized (Reference)
─────────────────────────────────        ─────────────────────────────────
ai-agent/work/NNN-concept-name/          ai-agent/concepts/[name]/
├── [working documents]            ──▶   ├── v1/
└── [session logs]                       │   ├── CONCEPT.md
                                         │   ├── CONCEPT-[sub].md
                                         │   └── ...
                                         └── v2/ (if major revision)
                                             └── ...

                                         ai-agent/workplans/[name]/
                                         ├── v1/
                                         │   ├── WORKPLAN.md
                                         │   ├── ROADMAP.md
                                         │   └── ROADMAP.mermaid.md
                                         └── v2/ (if major revision)
                                             └── ...
```

### Working Folder Structure (During Creation)

```
ai-agent/work/NNN-concept-name/
├── 00-OVERVIEW.md                  ← SSOT for concept work status
├── 01-INPUTS/                      ← Raw input folder
│   ├── INDEX.md                    ← Inventory of all inputs
│   └── [source files]              ← Raw files (copied/linked/fetched)
├── 02-EXTRACTIONS.md               ← Extracted information from inputs
├── 03-CONCEPT.md                   ← Main concept document
├── 03-CONCEPT-[subconcept].md      ← Sub-concept documents (max 7)
├── 04-WORKPLAN.md                  ← Work breakdown structure
├── 05-ROADMAP.md                   ← Sequencing and dependencies
├── 05-ROADMAP.mermaid.md           ← Generated Mermaid visualization
├── 06-PROGRESS-LOG.md              ← Session log (append-only)
├── 07-REFINEMENT-LOG.md            ← Tracks refinement cycles
└── 08-OPEN-QUESTIONS.md            ← Questions awaiting human input
```

### Finalized Folder Structure

When concept work is complete, outputs are promoted:

```
ai-agent/
├── concepts/                       ← Finalized concepts (like knowledge/)
│   └── [project-name]/
│       ├── v1/
│       │   ├── CONCEPT.md
│       │   ├── CONCEPT-[sub].md
│       │   └── INPUTS-SUMMARY.md   ← Summary of sources used
│       └── v2/                     ← Major revision (new inputs, big changes)
│           └── ...
├── workplans/                      ← Finalized work plans
│   └── [project-name]/
│       ├── v1/
│       │   ├── WORKPLAN.md
│       │   ├── ROADMAP.md
│       │   └── ROADMAP.mermaid.md
│       └── v2/
│           └── ...
├── work/                           ← Active work (existing)
└── knowledge/                      ← Project knowledge (existing)
```

---

## Document Guidelines

### Length Guidelines (Flexible)

| Document | Target Length | Notes |
|----------|---------------|-------|
| 00-OVERVIEW.md | ~2 pages | Keep scannable |
| 01-INPUTS/INDEX.md | Unlimited | Grows with inputs |
| 02-EXTRACTIONS.md | ~5 pages | Split if larger |
| 03-CONCEPT.md | ~4 pages | Can exceed if needed |
| 03-CONCEPT-*.md | ~3 pages each | Max 7 sub-concepts |
| 04-WORKPLAN.md | ~5 pages | Depends on complexity |
| 05-ROADMAP.md | ~3 pages | Plus Mermaid file |
| 06-PROGRESS-LOG.md | Unlimited | Append-only |
| 07-REFINEMENT-LOG.md | Unlimited | Tracks all changes |
| 08-OPEN-QUESTIONS.md | As needed | Cleared when answered |

**Important**: These are guidelines for readability. If the concept genuinely needs more space, exceed them. Quality and completeness over arbitrary limits.

---

## Workflow Commands

### Concept Commands

| Command | Purpose |
|---------|---------|
| `>>start concept name` | Initialize concept work |
| `>>add-input [path/url]` | Add input source to analysis |
| `>>extract` | Process inputs and extract information |
| `>>conceptualize` | Build/refine concept from extractions |
| `>>plan` | Generate work plan (asks for format first) |
| `>>roadmap` | Generate/update roadmap with Mermaid |
| `>>refine [phase]` | Enter refinement cycle at specified phase |
| `>>finalize` | Promote concept/workplan to top-level folders |
| `>>new-version` | Create new version for major revision |

### Existing Commands (Work As Expected)
- `>>continue` - Resume concept work
- `>>wrap` - End session with handoff
- `>>checkpoint` - Mid-session knowledge capture
- `>>status` - Show concept progress
- `>>archive` - Archive completed concept work folder

### Intelligent Command Detection

**Agent Behavior**: When human provides input without an explicit `>>` command, the agent should:
1. Analyze the prompt for intent
2. If it matches a command purpose with confidence, follow that workflow
3. If uncertain, ask: "This sounds like you want to [action]. Should I proceed with `>>[command]`?"

**Examples**:
- "Here's a PDF about the requirements" → Treat as `>>add-input`
- "Let's think through what this system needs to do" → Treat as `>>conceptualize`
- "Can you break this down into tasks?" → Treat as `>>plan`

---

## Detailed Phase Workflows

### Phase 1: GATHER (`>>start concept` + `>>add-input`)

**Trigger**: `>>start concept project-name`

**Protocol**:
1. Create concept work folder: `ai-agent/work/NNN-concept-name/`
2. Create initial documents:
   - `00-OVERVIEW.md` with status "Gathering"
   - `01-INPUTS/INDEX.md` empty inventory
   - `08-OPEN-QUESTIONS.md` template
3. Ask human about input sources
4. **Checkpoint consideration**: After creating structure, assess if checkpoint needed

**Adding Inputs**: `>>add-input path/to/file` or `>>add-input https://url`

For each input:
1. **URL handling**: Fetch content and save locally
2. **PDF handling**: Attempt extraction, ask human to confirm accuracy
3. Copy/link file to `01-INPUTS/`
4. Add entry to `01-INPUTS/INDEX.md`:
   ```markdown
   ## [Input Name]
   - **Source**: [path or URL]
   - **Type**: [conversation/document/pdf/web/other]
   - **Size**: [lines/pages/words estimate]
   - **Added**: [date]
   - **Status**: [ ] Not processed | [~] Processing | [x] Extracted
   - **Processing Notes**: [Any issues or considerations]
   - **Summary**: [Brief description - filled after extraction]
   ```

**Large Input Handling** (10000+ lines):
- Do NOT summarize or skip content
- Process in chunks with full attention
- Track progress in INDEX.md
- Multiple extraction sessions if needed
- Preserve all details - every message matters

---

### Phase 2: EXTRACT (`>>extract`)

**Trigger**: `>>extract` or `>>extract [input-name]`

**Protocol**:
1. **Checkpoint consideration**: Before starting large extraction, assess context usage
2. For each unprocessed input:
   - Parse content based on type
   - For large inputs: process methodically, chunk by chunk
   - Extract with categories below
   - Update INDEX.md status
3. Compile into `02-EXTRACTIONS.md`
4. Surface questions to `08-OPEN-QUESTIONS.md`
5. **Cross-reference check**: Ensure all sources are attributed
6. Present summary and questions to human

**Extraction Categories**:
```markdown
# Extractions

## Source Attribution
| ID | Theme/Item | Sources |
|----|------------|---------|
| T1 | [Theme] | input-1:L100-150, input-2:section-3 |

## Themes & Patterns
- **[T1] Theme Name**: [Description]
  - Sources: [input-1:lines, input-2:section]
  - Related: T2, T3

## Requirements
- **[R1]**: [Description]
  - Source: [input:location]
  - Priority: [High/Medium/Low]
  - Dependencies: [R2, R3]

## Constraints
- **[C1]**: [Description]
  - Source: [input:location]
  - Impact: [What this limits]

## Stakeholders
- **[S1] Role**: [Interest and influence]
  - Source: [input:location]

## Decisions Already Made
- **[D1]**: [Decision]
  - Source: [input:location]
  - Rationale: [Why]

## Contradictions & Ambiguities
- **[A1]**: [Description]
  - Sources: [input-1:loc vs input-2:loc]
  - Resolution needed: [Yes/No]

## Open Questions (move to 08-OPEN-QUESTIONS.md)
```

---

### Phase 3: CONCEPTUALIZE (`>>conceptualize`)

**Trigger**: `>>conceptualize`

**Protocol**:
1. Review `02-EXTRACTIONS.md`
2. **Checkpoint consideration**: Assess context before deep work
3. Structure concept:
   - Identify main concept scope
   - Identify sub-concepts (max 7, or split)
   - Define relationships
4. Create/update `03-CONCEPT.md`:

```markdown
# Concept: [Name]

## Vision
[What this achieves - 2-3 sentences]

## Scope
### In Scope
- [Item 1]
- [Item 2]

### Out of Scope
- [Item 1] - Rationale: [Why excluded]

### Scope Boundaries
[Clear description of where this concept ends]

## Sub-Concepts
| Sub-Concept | Document | Status | Description |
|-------------|----------|--------|-------------|
| [Name] | [03-CONCEPT-name.md](03-CONCEPT-name.md) | Draft/Review/Final | [Brief] |

**Note**: Maximum 7 sub-concepts. If more needed, consider splitting into multiple concept efforts.

## Core Concept
### [Aspect 1]
[Description with source references: (R1, T2)]

### [Aspect 2]
[Description]

## Non-Technical Aspects
### Process Changes
- [Change 1] (Source: T3)

### Communication Needs
- [Need 1]

### Training/Documentation Needs
- [Item 1]

## Dependencies
### External
- [Dependency 1]

### Internal
- [Dependency 1]

## Risks & Mitigations
| ID | Risk | Likelihood | Impact | Mitigation |
|----|------|------------|--------|------------|
| RK1 | [Risk] | H/M/L | H/M/L | [Strategy] |

## Success Criteria
- [ ] [Criterion 1] (maps to R1)
- [ ] [Criterion 2]

## Traceability
| Concept Element | Source Requirements | Source Themes |
|-----------------|---------------------|---------------|
| [Element] | R1, R3 | T1, T2 |

## Open Questions
→ See [08-OPEN-QUESTIONS.md](08-OPEN-QUESTIONS.md)
```

5. Create sub-concept documents as needed (max 7)
6. **Cross-reference update**: Update all traceability links
7. Present to human for feedback
8. **Proactive refinement check**: Flag any inconsistencies with extractions

---

### Phase 4: PLAN (`>>plan`)

**Trigger**: `>>plan`

**Protocol**:
1. **Ask format first**:
   ```
   What format would you like for the work plan?
   - `generic` - Flexible phases/work-packages/tasks
   - `jira` - Epics/Stories (with optional sub-tasks)
   - `github` - Issues with labels and milestones
   - `custom` - Describe your structure
   ```
2. Wait for human response
3. Generate `04-WORKPLAN.md` in chosen format
4. **Cross-reference update**: Link to concept elements
5. Present for feedback

**Generic Format**:
```markdown
# Work Plan: [Concept Name]

## Overview
- **Total Phases**: [N]
- **Total Work Packages**: [N]
- **Estimated Complexity**: [High/Medium/Low]

## Traceability Matrix
| Work Package | Concept Elements | Requirements |
|--------------|------------------|--------------|
| WP 1.1 | Section 3.1 | R1, R2 |

---

## Phase 1: [Name]
**Objective**: [What this phase achieves]
**Concept Reference**: [Which concept sections]

### WP 1.1: [Work Package Name]
**Description**: [What this delivers]
**Complexity**: [High/Medium/Low]
**Dependencies**: [None | WP X.X]
**Concept Trace**: [Concept section/element]

#### Tasks
- [ ] **T1.1.1**: [Description]
  - Type: [Development/Clarification/Documentation/Other]
- [ ] **T1.1.2**: [Description]

### WP 1.2: [Work Package Name]
...

---

## Phase 2: [Name]
...
```

**Jira Format**:
```markdown
# Work Plan: [Concept Name] (Jira Format)

## Epic 1: [Name]
**Key**: [PROJECT-EPIC-1]
**Summary**: [Epic description]
**Labels**: [label1, label2]
**Concept Trace**: [Concept section]

### Story 1.1: [Name]
**Summary**: [Story description]
**Story Points**: [Estimate]
**Acceptance Criteria**:
- [ ] Criterion 1
- [ ] Criterion 2

**Sub-tasks** (optional):
- [ ] Sub-task 1
- [ ] Sub-task 2

### Story 1.2: [Name]
...

## Epic 2: [Name]
...
```

---

### Phase 5: ROADMAP (`>>roadmap`)

**Trigger**: `>>roadmap`

**Protocol**:
1. Analyze dependencies from `04-WORKPLAN.md`
2. Generate `05-ROADMAP.md`:

```markdown
# Roadmap: [Concept Name]

## Dependency Analysis

### Critical Path
[Description of the longest dependency chain]

### Parallel Opportunities
[What can be done simultaneously]

## Sequence Waves

### Wave 1: Foundation (Can start immediately)
| Work Package | Description | Enables |
|--------------|-------------|---------|
| WP 1.1 | [Name] | WP 1.2, WP 2.1 |
| WP 1.4 | [Name] | WP 2.2 |

### Wave 2: Core (After Wave 1)
| Work Package | Description | Depends On | Enables |
|--------------|-------------|------------|---------|
| WP 1.2 | [Name] | WP 1.1 | WP 2.1 |
| WP 1.3 | [Name] | WP 1.1 | WP 2.2 |

### Wave 3: Integration (After Wave 2)
| Work Package | Description | Depends On |
|--------------|-------------|------------|
| WP 2.1 | [Name] | WP 1.2 |
| WP 2.2 | [Name] | WP 1.3, WP 1.4 |

## Milestones
| Milestone | Description | After Wave | Success Criteria |
|-----------|-------------|------------|------------------|
| M1 | [Name] | Wave 1 | [Criteria] |
| M2 | [Name] | Wave 3 | [Criteria] |

## Risk Points
- **Bottleneck at WP X.X**: [Why and mitigation]
```

3. Generate `05-ROADMAP.mermaid.md`:

```markdown
# Roadmap Visualization

> **Note**: This file is auto-generated. Edit 05-ROADMAP.md for changes.

## Dependency Graph

​```mermaid
graph LR
    subgraph Wave1[Wave 1: Foundation]
        WP1.1[WP 1.1: Name]
        WP1.4[WP 1.4: Name]
    end

    subgraph Wave2[Wave 2: Core]
        WP1.2[WP 1.2: Name]
        WP1.3[WP 1.3: Name]
    end

    subgraph Wave3[Wave 3: Integration]
        WP2.1[WP 2.1: Name]
        WP2.2[WP 2.2: Name]
    end

    WP1.1 --> WP1.2
    WP1.1 --> WP1.3
    WP1.2 --> WP2.1
    WP1.3 --> WP2.2
    WP1.4 --> WP2.2

    M1((M1)) -.-> Wave1
    M2((M2)) -.-> Wave3
​```

## Timeline View (if dates added)

​```mermaid
gantt
    title Project Roadmap
    dateFormat YYYY-MM-DD

    section Wave 1
    WP 1.1: wp11, 2025-01-01, 2w
    WP 1.4: wp14, 2025-01-01, 1w

    section Wave 2
    WP 1.2: wp12, after wp11, 2w
    WP 1.3: wp13, after wp11, 1w

    section Wave 3
    WP 2.1: wp21, after wp12, 2w
    WP 2.2: wp22, after wp13 wp14, 3w
​```
```

4. Present to human for review

---

### Phase 6: REFINE (`>>refine [phase]`)

**Trigger**: `>>refine extract` | `>>refine concept` | `>>refine plan` | `>>refine roadmap`

**Protocol**:
1. Log in `07-REFINEMENT-LOG.md`:
   ```markdown
   ## Refinement Cycle [N]
   **Date**: [date]
   **Entry Point**: [phase]
   **Trigger**: [What caused this - human request or agent detection]
   **Version**: [current version]

   ### Changes Made
   #### [Phase Name]
   - [Specific change with before/after if significant]

   #### Cascaded to [Next Phase]
   - [Consequent change]

   ### Cross-Reference Updates
   - [ ] Updated traceability in [doc]
   - [ ] Updated source references in [doc]

   ### Impact Assessment
   - [Impact 1]
   - [Impact 2]
   ```

2. Apply changes to entry phase
3. **Cascade forward** (CRITICAL):
   - `extract` → concept → plan → roadmap
   - `concept` → plan → roadmap
   - `plan` → roadmap
   - `roadmap` → only roadmap
4. **Update ALL cross-references** in affected documents
5. Update `00-OVERVIEW.md`
6. Notify human of all cascading changes

**Proactive Refinement Detection**:
Agent should suggest refinement when detecting:
- Inconsistencies between documents
- New information contradicting existing content
- Gaps in traceability
- Scope changes implied by recent inputs

---

### Phase 7: FINALIZE (`>>finalize`)

**Trigger**: `>>finalize`

**Protocol**:
1. Verify completeness:
   - All inputs processed
   - No unresolved questions in `08-OPEN-QUESTIONS.md`
   - Concept, workplan, and roadmap complete
2. Determine version:
   - Check if `ai-agent/concepts/[name]/` exists
   - If new: create `v1/`
   - If exists: create next version `vN/`
3. Copy finalized documents:
   - Concept docs → `ai-agent/concepts/[name]/vN/`
   - Workplan + roadmap → `ai-agent/workplans/[name]/vN/`
4. Create `INPUTS-SUMMARY.md` in concept folder
5. Update working folder status to "Finalized"
6. Archive or keep working folder (ask human)

---

### Version Management (`>>new-version`)

**Trigger**: `>>new-version` (for major revisions with significant new inputs)

**When to use**:
- Weeks have passed with significant changes
- New major inputs (meetings, discoveries)
- Fundamental direction change

**Protocol**:
1. Create new work folder: `NNN-concept-name-v2`
2. Copy current state as starting point
3. Reference previous version in `00-OVERVIEW.md`
4. Fresh `07-REFINEMENT-LOG.md` for new version
5. Process new inputs through full workflow

---

## Open Questions Workflow

### The 08-OPEN-QUESTIONS.md Document

```markdown
# Open Questions: [Concept Name]

> Instructions: Agent adds questions below. Human adds answers in the
> "Human Response" sections. Run `>>continue` after answering for agent
> to process responses.

---

## Questions from Extraction Phase

### Q1: [Question about input interpretation]
**Context**: [Why this question arose]
**Source**: [Which input, location]
**Impact**: [What depends on the answer]

#### Human Response
<!-- Add your answer below this line -->


<!-- End of response -->

---

### Q2: [Another question]
...

---

## Questions from Conceptualization Phase

### Q3: [Question about concept scope]
...

---

## Resolved Questions Archive

### [Archived questions with answers, for reference]
```

**Agent Behavior**:
- Add questions with full context
- After human answers, process and update relevant documents
- Move resolved questions to archive section
- Update cross-references

---

## Challenges & Mitigations (Updated)

### Challenge 1: Input Format Diversity (UPDATED)
**Problem**: Various formats need different handling, especially large conversations.

**Mitigations**:
- URL fetching supported - save locally
- PDF extraction attempted with human confirmation
- **Large conversations (10000+ lines)**:
  - Process in full - every message matters
  - Chunk processing with progress tracking
  - Multiple sessions if needed
  - NO summarization or skipping
  - Track extraction progress in INDEX.md

### Challenge 2: Concept Scope Creep (UPDATED)
**Problem**: Concepts can grow unbounded.

**Mitigations**:
- Explicit In/Out of Scope sections
- Sub-concept documents (max 7 before splitting)
- Regular scope reviews during refinement
- **Flexible length limits** - guidelines not rules
- Split into multiple concept efforts if > 7 sub-concepts

### Challenge 3: Traceability Loss (UPDATED)
**Problem**: Changes break links between documents.

**Mitigations**:
- Source attribution with IDs (T1, R1, etc.)
- Traceability matrices in concept and workplan
- Refinement log tracks all changes
- **CRITICAL**: Agent must update cross-references on EVERY change
- Explicit cross-reference checklist in refinement workflow

### Challenge 4: Over-Engineering vs Under-Specification
**Problem**: Concepts too abstract or too detailed.

**Mitigations**:
- Clear phase gates with human approval
- Explicit Open Questions workflow
- Allow partial completion
- Complexity indicators for calibration

### Challenge 5: Context Window Limits (UPDATED)
**Problem**: Complex concepts may exceed context.

**Mitigations**:
- **Flexible document lengths** - split if too large
- **Proactive checkpoints** - agent decides when to checkpoint:
  - Before large extraction tasks
  - Before deep conceptualization
  - When context usage high
  - Agent announces: "I'll set a checkpoint before proceeding with [task]"
- Modular structure (sub-concepts in separate files)
- Summary sections for quick context recovery

### Challenge 6: Human-AI Alignment
**Problem**: Misunderstanding abstract requirements.

**Mitigations**:
- Extract phase surfaces questions early
- Contradiction/ambiguity detection
- Multiple checkpoints for human review
- Refinement cycles for correction
- **Proactive inconsistency detection**

### Challenge 7: Work Plan Format Flexibility (UPDATED)
**Problem**: Different organizations use different structures.

**Mitigations**:
- **Always ask format preference before generating**
- Generic, Jira, GitHub formats supported
- Custom format option
- Clear mapping documentation

---

## Integration with Existing System

### Folder Structure Addition
```
ai-agent/
├── meta/           ← Existing
├── work/           ← Existing (concept work starts here)
├── knowledge/      ← Existing
├── concepts/       ← NEW: Finalized concepts
│   └── [name]/v1/
└── workplans/      ← NEW: Finalized work plans
    └── [name]/v1/
```

### Knowledge Updates During Concept Work
Concepts generate reusable knowledge:
- Domain concepts → `knowledge/CONCEPTS-INDEX.md`
- Technical patterns → `knowledge/subsystems/`
- Useful commands → `knowledge/COMMANDS.md`

### Transition to Implementation
When concept is complete:
1. Finalize concept (`>>finalize`)
2. Create implementation work items referencing concept:
   - `>>start feat [name]` - Reference: `concepts/[name]/v1/`
3. Work plan guides implementation phases

---

## Success Criteria

A concept workflow is successful when:

- [ ] All input sources inventoried and fully processed (no skipping)
- [ ] Extractions capture all details with source attribution
- [ ] Concept is structured with ≤7 sub-concepts
- [ ] All cross-references are maintained
- [ ] Open questions are resolved
- [ ] Work plan in appropriate format
- [ ] Roadmap has dependency graph and Mermaid visualization
- [ ] Refinement cycles tracked with cascade effects
- [ ] Human approves each phase output
- [ ] Finalized artifacts in top-level folders

---

## Next Steps

1. ✅ Review feedback and update concept (this document)
2. ✅ Create templates for all concept documents
3. ✅ Update FOR-AGENTS.md with concept protocols
4. ✅ Update FOR-HUMANS.md with concept workflow guide
5. ✅ Update meta/README.md with new folder structure
6. [ ] Test with a real concept project
