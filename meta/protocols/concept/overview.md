# Concept Workflow Overview

**Purpose**: Complex conceptualization work - analyzing inputs, building concepts, creating work plans, and generating roadmaps.

---

## Concept Workflow Phases

```
Gathering → Extracting → Conceptualizing → Planning → Roadmapping → Finalizing
```

| Phase | Command | Output |
|-------|---------|--------|
| Gathering | `>>start concept`, `>>add-input` | 01-INPUTS/INDEX.md |
| Extracting | `>>extract` | 02-EXTRACTIONS.md |
| Conceptualizing | `>>conceptualize` | 03-CONCEPT.md, sub-concepts |
| Planning | `>>plan` | 04-WORKPLAN.md |
| Roadmapping | `>>roadmap` | 05-ROADMAP.md, mermaid |
| Finalizing | `>>finalize` | Promoted to concepts/, workplans/ |

---

## Concept Work Structure

```
ai-agent/work/NNN-concept-name/
├── 00-OVERVIEW.md             ← SSOT for concept work
├── 01-INPUTS/
│   └── INDEX.md               ← Input inventory
├── 02-EXTRACTIONS.md          ← Extracted information
├── 03-CONCEPT.md              ← Main concept
├── 03-CONCEPT-[sub].md        ← Sub-concepts (max 7)
├── 04-WORKPLAN.md             ← Work breakdown
├── 05-ROADMAP.md              ← Sequencing
├── 05-ROADMAP.mermaid.md      ← Visual diagram
├── 06-PROGRESS-LOG.md         ← Session log
├── 07-REFINEMENT-LOG.md       ← Refinement tracking
├── 08-OPEN-QUESTIONS.md       ← Questions for human
└── 90-OUTPUTS/                ← Deliverables
```

---

## Finalized Output Structure

After `>>finalize`:

```
ai-agent/concepts/[name]/v1/
├── CONCEPT.md
├── CONCEPT-[sub].md
└── INPUTS-SUMMARY.md

ai-agent/workplans/[name]/v1/
├── WORKPLAN.md
├── ROADMAP.md
└── ROADMAP.mermaid.md
```

---

## Intelligent Command Detection

When human provides input without explicit `>>` command:

1. Analyze the prompt for intent
2. If it matches a command purpose with confidence, follow that workflow
3. If uncertain, ask: "This sounds like you want to [action]. Should I proceed with `>>[command]`?"

**Examples**:
- "Here's a PDF about the requirements" → Treat as `>>add-input`
- "Let's think through what this system needs to do" → Treat as `>>conceptualize`
- "Can you break this down into tasks?" → Treat as `>>plan`

---

## Refinement Cycles

Use `>>refine [phase]` to re-enter workflow at any phase:
- Changes cascade forward automatically
- All cross-references updated
- Tracked in 07-REFINEMENT-LOG.md

---

## Concept Protocols

| Command | Protocol |
|---------|----------|
| `>>start concept` | [start-concept.md](start-concept.md) |
| `>>add-input` | [add-input.md](add-input.md) |
| `>>extract` | [extract.md](extract.md) |
| `>>conceptualize` | [conceptualize.md](conceptualize.md) |
| `>>plan` | [plan.md](plan.md) |
| `>>roadmap` | [roadmap.md](roadmap.md) |
| `>>refine` | [refine.md](refine.md) |
| `>>finalize` | [finalize.md](finalize.md) |
| `>>new-version` | [new-version.md](new-version.md) |

---

## Key Principles

1. **Source Attribution**: All extractions reference source inputs (T1, R2, etc.)
2. **Traceability**: Concept elements link back to requirements
3. **Max Sub-concepts**: Limit to 7; suggest splitting if more needed
4. **Cascade Forward**: Refinements propagate to all downstream documents
5. **Open Questions**: Surface ambiguities in 08-OPEN-QUESTIONS.md
