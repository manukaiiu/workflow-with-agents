# Protocol: >>conceptualize

**Trigger**: `>>conceptualize` or "let's build the concept", "create the concept"
**Purpose**: Build concept document from extractions

---

## Protocol Steps

### 1. Review Extractions

Read `02-EXTRACTIONS.md`:
- Understand all themes, requirements, constraints
- Note decisions already made
- Check for unresolved ambiguities

### 2. Checkpoint Consideration

Before deep conceptualization work:
- Assess context usage
- If high, run `>>checkpoint` first

### 3. Structure the Concept

Identify:
- Main concept scope
- Sub-concepts (max 7)
- Relationships and dependencies

If more than 7 sub-concepts needed:
```
Note: Identified [N] potential sub-concepts, but maximum is 7.
Suggest either:
1. Combine related concepts
2. Split into separate concept work items

Which approach would you prefer?
```

### 4. Create/Update 03-CONCEPT.md

```markdown
# Concept: [Name]

**Version**: 1.0
**Last Updated**: [Date]
**Status**: Draft

## Vision
[2-3 sentences describing what this concept achieves]

## Scope

### In Scope
| Item | Source | Rationale |
|------|--------|-----------|
| [Item 1] | R1, T2 | [Why included] |
| [Item 2] | R3 | [Why included] |

### Out of Scope
| Item | Rationale |
|------|-----------|
| [Item 1] | [Why excluded] |
| [Item 2] | [Why excluded] |

## Sub-Concepts

| Sub-Concept | Document | Purpose |
|-------------|----------|---------|
| [Name 1] | 03-CONCEPT-[name1].md | [Brief purpose] |
| [Name 2] | 03-CONCEPT-[name2].md | [Brief purpose] |

## Core Concept

### [Section 1 Name]
**Sources**: T1, R2, R5

[Detailed description with references to extraction IDs]

### [Section 2 Name]
**Sources**: T3, R7, C2

[Detailed description]

## Non-Technical Aspects
- [Stakeholder considerations]
- [Process implications]
- [Organizational impacts]

## Dependencies
| Dependency | Type | Impact |
|------------|------|--------|
| [Dep 1] | External/Internal | [What it affects] |

## Risks & Mitigations
| Risk | Likelihood | Impact | Mitigation |
|------|------------|--------|------------|
| [Risk 1] | High/Med/Low | High/Med/Low | [How to address] |

## Success Criteria
- [ ] [Criterion 1]
- [ ] [Criterion 2]
- [ ] [Criterion 3]

## Traceability Matrix
| Concept Element | Requirements | Themes |
|-----------------|--------------|--------|
| [Element 1] | R1, R3 | T1 |
| [Element 2] | R2, R5 | T2, T4 |
```

### 5. Create Sub-Concept Documents

For each sub-concept (max 7):
- Create `03-CONCEPT-[name].md`
- Link from main concept
- Include source references

```markdown
# Sub-Concept: [Name]

**Parent**: 03-CONCEPT.md
**Sources**: [Relevant extraction IDs]

## Purpose
[What this sub-concept covers]

## Details
[Detailed description]

## Interfaces
- Connects to: [Other sub-concepts]
- Dependencies: [What it needs]
- Provides: [What it offers]
```

### 6. Cross-Reference Update

Ensure all traceability links work:
- Concept elements → Extraction IDs
- Sub-concepts → Parent concept
- Requirements coverage complete

### 7. Proactive Refinement Check

Flag any inconsistencies:
- Missing requirements coverage
- Contradictions with extractions
- Gaps in concept

### 8. Present to Human

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

## Related Protocols

- Extracting inputs → [extract.md](extract.md)
- Creating work plan → [plan.md](plan.md)
- Refinement → [refine.md](refine.md)
