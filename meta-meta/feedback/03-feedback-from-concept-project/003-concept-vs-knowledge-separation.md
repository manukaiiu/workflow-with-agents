# Feedback: Concept Work vs Knowledge Work - Clarify Separation

**ID**: FB-003
**Date**: 2025-12-09
**Source Project**: AID-CC Concept Work
**Category**: Workflow Design / Work Type Definition
**Priority**: High

---

## Observation

When starting this project, there was confusion between:
- **Knowledge work** (`init-knowledge`): Documenting understanding for future reference
- **Concept work** (`concept`): Synthesizing inputs into actionable plans

The workflow system's initial prompt suggested knowledge creation, but the actual need was concept work leading to a work plan.

## The Fundamental Difference

| Aspect | Knowledge Work | Concept Work |
|--------|----------------|--------------|
| **Purpose** | Document understanding | Plan action |
| **Output** | Reference documentation | Decisions + Work plan |
| **Orientation** | Past/Present ("what is") | Future ("what to do") |
| **Lifespan** | Long-lived, maintained | Project-scoped, evolves into execution |
| **Trigger** | "I need to understand X" | "I need to build/do X" |
| **Success** | Can answer questions later | Can execute the plan |

## The AID-CC Case

This project has **both needs**, which added to the confusion:

### Knowledge Needs (per Work Package)
Each WP may develop its own knowledge base over time:
- **WP2 Knowledge**: Clinical data structures, ontologies, KG patterns
- **WP3 Knowledge**: Platform architecture, component library, API contracts
- **WP4 Knowledge**: Trustworthy AI frameworks, regulatory requirements
- **WP5 Knowledge**: Healthcare standards (HL7, FHIR), integration patterns

### Concept Need (what we did)
- Synthesize project inputs → System concept
- Break down into work packages → Sub-concepts
- Generate actionable plan → JIRA-compatible work plan

## The Problem

1. **Workflow didn't distinguish clearly**: `>>start` defaulted toward knowledge capture
2. **Multi-WP projects are complex**: Each WP could have its own knowledge base
3. **Concept work consumes knowledge but isn't knowledge**: We read documents (knowledge inputs) to produce a plan (concept output)
4. **Lifecycle difference unclear**: Knowledge persists; concepts evolve into work then archive

## Suggested Clarifications

### 1. Clearer Work Type Triggers

| User Intent | Work Type | Trigger Phrases |
|-------------|-----------|-----------------|
| "Document what I learned" | `init-knowledge` | "understand", "document", "learn about" |
| "Plan what to build" | `concept` | "plan", "design", "figure out how to", "create a work plan" |
| "Build the thing" | `feature` | "implement", "build", "add", "create" |

### 2. Concept → Knowledge Relationship

```
Concept Work                          Knowledge Work
─────────────                         ──────────────
┌─────────────┐                       ┌─────────────┐
│   INPUTS    │ ──── may feed ────►   │  KNOWLEDGE  │
│ (documents, │      into             │    BASE     │
│  research)  │                       │             │
└──────┬──────┘                       └──────▲──────┘
       │                                     │
       ▼                                     │
┌─────────────┐                              │
│   CONCEPT   │                              │
│   (plan)    │                              │
└──────┬──────┘                              │
       │                                     │
       ▼                                     │
┌─────────────┐      learnings              │
│  EXECUTION  │ ──── documented ────────────┘
│   (work)    │      during work
└─────────────┘
```

### 3. Multi-WP Knowledge Structure

For projects with multiple work packages, knowledge could be structured:

```
ai-agent/knowledge/
├── 00-PROJECT-OVERVIEW.md      # Cross-WP knowledge
├── wp1-project-management/     # WP-specific knowledge
├── wp2-knowledge-base/
├── wp3-platform/
├── wp4-trustworthy-ai/
├── wp5-integration/
└── wp6-education/
```

This parallels how concept sub-documents work (03-CONCEPT-WP3.md, etc.)

### 4. Workflow Guidance Update

In `FOR-AGENTS.md`, add decision guidance:

```markdown
## Choosing Work Type

Ask yourself:
1. Is the goal to **document understanding** for future reference?
   → Use `init-knowledge` or `knowledge` work type

2. Is the goal to **decide what to build** and create a plan?
   → Use `concept` work type

3. Is the goal to **build something** based on an existing plan?
   → Use `feature`, `bug`, or `maintenance` work type

Note: Concept work often *consumes* knowledge inputs but *produces*
plans, not documentation. Don't conflate the two.
```

## Recommendation

1. **Clarify in FOR-AGENTS.md**: Add explicit guidance on concept vs knowledge distinction
2. **Add workflow prompts**: When `>>start` is invoked, ask clarifying questions if intent is ambiguous
3. **Support WP-scoped knowledge**: For multi-WP projects, allow knowledge to be organized by work package
4. **Document the lifecycle**: Concept → Execution → Knowledge feedback loop

---

## Meta

**Feedback Type**: Workflow Design
**Affects**: FOR-AGENTS.md, work type definitions, `>>start` behavior
**Root Cause**: Implicit assumption that "processing inputs" = "knowledge work"
**Pattern**: Distinguish "understand for reference" vs "understand to act"
