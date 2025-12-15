# Feedback: Extraction ID Prefixes Need Glossary

**ID**: FB-001
**Date**: 2025-12-09
**Source Project**: AID-CC Concept Work
**Category**: Documentation / Templates
**Priority**: Medium

---

## Observation

During concept work, the agent (me) used single-letter prefixes in `02-EXTRACTIONS.md` to categorize extracted information:

| Prefix | Meaning |
|--------|---------|
| T | Theme |
| R | Requirement |
| C | Constraint |
| S | Stakeholder |
| D | Decision |
| A | Ambiguity |

The human collaborator asked "What do T, R and C stand for?" - indicating these abbreviations were not self-explanatory.

## Problem

1. **Implicit knowledge**: The prefix system was invented ad-hoc without documentation
2. **Discoverability**: No legend or glossary in the template or output
3. **Consistency risk**: Future agents may invent different prefixes for the same concepts
4. **Accumulation**: More abbreviations will likely emerge across different work types

## Suggested Solution

### Option A: Template-Level Glossary

Add a `## Glossary` section to the `02-EXTRACTIONS.md` template with predefined prefixes:

```markdown
## Glossary

| Prefix | Category | Description |
|--------|----------|-------------|
| T | Theme | Recurring patterns or concepts across inputs |
| R | Requirement | Specific requirements that must be met |
| C | Constraint | Limitations or boundaries on the work |
| S | Stakeholder | People or groups with interest in the outcome |
| D | Decision | Choices already made that constrain the solution |
| A | Ambiguity | Contradictions or unclear areas needing resolution |
| Q | Question | Open questions requiring human input |
```

### Option B: Workflow-Level Glossary

Create a shared glossary file at `ai-agent/meta/GLOSSARY.md` that:
- Defines standard prefixes across all work types
- Is referenced from templates
- Can be extended as new prefixes emerge
- Agents are instructed to consult and update it

### Option C: Inline Legends

Require agents to include a brief legend at the start of any table using abbreviations.

## Recommendation

**Option B** (Workflow-Level Glossary) is most scalable:
- Single source of truth for abbreviations
- Prevents drift across projects
- Easy for agents to reference and extend
- Supports accumulation of terminology over time

## Additional Consideration

The glossary could also capture:
- Status indicators (`[ ]`, `[x]`, `[~]`)
- Priority levels (H/M/L)
- Work type abbreviations
- Any other conventions that emerge

---

## Meta

**Feedback Type**: Process Improvement
**Affects**: `ai-agent/meta/templates/concept/02-EXTRACTIONS.md`
**Related Files**: All extraction templates across work types
