# Feedback: Process/Management Work Type for Workflow System

**ID**: FB-006
**Date**: 2025-12-11
**Source Project**: WP4 Expert Involvement Process (002-concept-expert-involvement)
**Category**: Workflow System / Work Types
**Priority**: Medium

---

## Observation

Work item 002 (Expert Involvement Process) was different from 001 (AID-CC System Concept):

| Aspect | 001: Technical Concept | 002: Process/Management |
|--------|------------------------|-------------------------|
| **Inputs** | Requirements docs, specs, PDFs | User prompt, discussions |
| **Outputs** | Concepts, work plans, roadmaps | Templates, strategies, guidelines |
| **Extraction** | Themes (T), Requirements (R), Constraints (C) | Goals, considerations, approaches |
| **Planning** | Epics, stories, story points | Action items, dependencies |
| **Artifacts** | Architecture specs, JIRA plans | Word templates, process flows |

The current workflow system in `FOR-AGENTS.md` is primarily designed for **technical concept work** with:
- Extraction IDs (T1, R1, C1...)
- Work plans with story points
- Technical roadmaps with dependencies

Work item 002 didn't naturally fit this structure - it was lighter, output-focused, and iterative by nature.

---

## Gap Analysis

### What Worked Well

1. **Work folder structure** - `002-concept-expert-involvement/` worked fine
2. **00-OVERVIEW.md** - Provided good status tracking
3. **01-INPUTS/** - Input tracking was useful even for simple inputs
4. **03-CONCEPT.md** - Concept document worked, though lighter than technical concepts

### What Didn't Fit

1. **02-EXTRACTIONS.md** - Not created; extraction IDs felt heavy for this work type
2. **04-WORKPLAN.md** - Not needed; no stories/points for process design
3. **05-ROADMAP.md** - Not needed; dependencies were sequential, not technical
4. **Extraction ID system** - T1, R1, C1 etc. didn't make sense for process work

### What Was Missing

1. **Deliverables folder** - Created `03-DELIVERABLES/` ad-hoc for templates
2. **Dependency tracking** - Created `work-sequence-and-dependencies.md` ad-hoc
3. **Bridging documents** - Created bridging input for next work item ad-hoc

---

## Suggested Solutions

### Option A: New Work Type `process`

Add a new work type for process/management work:

**Prefix**: `NNN-process-[name]`

**Folder Structure**:
```
NNN-process-[name]/
├── 00-OVERVIEW.md           ← Status tracking (lighter)
├── 01-CONTEXT.md            ← Background, goals, constraints
├── 02-APPROACH.md           ← Strategy and considerations
├── 03-DELIVERABLES/         ← Templates, guides, processes
├── 04-DEPENDENCIES.md       ← Work sequence, blockers
└── 05-LESSONS-LEARNED.md    ← Post-completion retrospective
```

**Characteristics**:
- No extraction IDs
- Output-focused (deliverables over analysis)
- Lighter documentation
- Iterative by design (improve after use)

### Option B: Mode Extension to `concept` Type

Keep single `concept` type but add modes:

```markdown
## Mode: technical | process

**Technical Mode** (default):
- Full extraction with IDs
- Work plan with story points
- Technical roadmap

**Process Mode**:
- Lighter extraction (no IDs)
- Output-focused deliverables
- Dependency tracking instead of roadmap
```

Signal mode in 00-OVERVIEW.md header:
```markdown
**Mode**: Process
```

### Option C: Flexible Concept Structure

Make concept workflow more flexible without explicit modes:

- Extraction IDs: Optional (use when inputs are complex)
- Work plan: Optional (use when implementation is significant)
- Roadmap: Optional (use when technical dependencies exist)
- Add: `03-DELIVERABLES/` as standard optional folder

---

## Recommendation

**Option B (Mode Extension)** is recommended because:

1. **Minimal change** - Extends existing system rather than adding new type
2. **Clear signal** - Mode marker in OVERVIEW.md is explicit
3. **Flexible** - Can still use any concept workflow element if needed
4. **Discoverable** - Agents see modes when reading FOR-AGENTS.md

### Suggested Implementation

Add to `FOR-AGENTS.md` in the Concept Work section:

```markdown
### Concept Work Modes

Concept work operates in one of two modes:

**Technical Mode** (default)
Use for: System concepts, architecture design, technical planning
- Full extraction phase with IDs (T1, R1, C1...)
- Work plan with epics, stories, story points
- Technical roadmap with dependencies
- Signal: `**Mode**: Technical` (or omit - it's default)

**Process Mode**
Use for: Process design, management work, templates, strategies
- Lighter extraction (goals, considerations - no IDs needed)
- Deliverables folder instead of work plan
- Dependency tracking instead of technical roadmap
- Signal: `**Mode**: Process`

**Choosing a Mode**
- If outputs are code specs, architecture, JIRA stories → Technical
- If outputs are templates, processes, strategies → Process
- If unclear → Start with Process, switch if complexity warrants Technical
```

Add standard folder for deliverables:

```markdown
### Optional Folders

**03-DELIVERABLES/** (Process Mode)
For work items producing templates, documents, or processes rather than
technical specifications. Contains the actual outputs of the work item.
```

---

## Additional Observations from This Work Item

### 1. Bridging Documents Are Valuable

Work item 002 created a "bridging input" document for the next work item. This pattern is useful:
- Captures context that would otherwise be lost between work items
- Defines inputs for the next phase
- Creates continuity

**Suggestion**: Add bridging documents as a recommended practice when one work item feeds directly into another.

### 2. Work Sequence Clarity

The `work-sequence-and-dependencies.md` document proved essential for understanding:
- What must happen before what
- Which work items are blocked
- How catalogue-integration-suggestions.md affects sequencing

**Suggestion**: For complex multi-work-item projects, consider a project-level dependency document.

### 3. External Document Alignment

Work item 002 initially created chapter references that didn't match the actual report structure. This was corrected when the `.txt` version of the report was provided.

**Suggestion**: When referencing external documents (Word, PDF), explicitly note the document version and consider keeping a text/markdown mirror in the repo for agent access.

---

## Impact Assessment

| If Implemented | Benefit |
|----------------|---------|
| Mode extension | Agents can handle both technical and process work naturally |
| Deliverables folder | Standard place for templates, guides |
| Bridging documents | Better continuity between work items |
| External doc alignment | Reduced errors from misaligned references |

---

## Related Feedback

- **FB-005**: Workflow loss in long sessions (context window summarization)
- This feedback (FB-006): Workflow doesn't fit process/management work

Together these suggest the workflow system needs:
1. Better resilience across context windows (FB-005)
2. Better flexibility for different work types (FB-006)

---

## Meta

**Feedback Type**: Workflow System Enhancement
**Affects**: `ai-agent/meta/FOR-AGENTS.md`
**Related Work Items**: 002-concept-expert-involvement
**Severity**: Medium - workarounds exist but add friction
