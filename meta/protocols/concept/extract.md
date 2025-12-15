# Protocol: >>extract

**Trigger**: `>>extract` or "let's extract from the inputs", "process the inputs"
**Purpose**: Process inputs and extract categorized information

---

## Protocol Steps

### 1. Checkpoint Consideration

Before starting large extraction, assess context usage:
- If high (~70%+), announce: "I'll set a checkpoint before proceeding with extraction."
- Use `>>checkpoint` protocol if needed

### 2. Process Each Unprocessed Input

For each input in INDEX.md marked `[ ] Not processed`:

1. Read content based on type
2. For large inputs: process methodically, chunk by chunk
3. Extract to categories (see below)
4. Update INDEX.md status to `[x] Extracted`

### 3. Extraction Categories

Extract information into these categories with IDs:

| Category | ID Prefix | Examples |
|----------|-----------|----------|
| Themes & Patterns | T1, T2... | Recurring ideas, patterns |
| Requirements | R1, R2... | What must be done/included |
| Constraints | C1, C2... | Limitations, restrictions |
| Stakeholders | S1, S2... | People/roles involved |
| Decisions Already Made | D1, D2... | Already decided items |
| Contradictions & Ambiguities | A1, A2... | Conflicts, unclear items |

### 4. Create/Update 02-EXTRACTIONS.md

```markdown
# Extractions

**Last Updated**: [Date]
**Inputs Processed**: [N] of [M]

## Source Attribution
| ID | Source Input | Location |
|----|--------------|----------|
| T1 | meeting-notes.md | Lines 45-52 |
| R1 | requirements-doc.md | Section 3.2 |

## Themes & Patterns
### T1: [Theme Name]
**Source**: [Input name, location]
[Description of theme]

### T2: [Theme Name]
...

## Requirements
### R1: [Requirement]
**Source**: [Input name, location]
**Priority**: [High/Medium/Low]
[Description]

### R2: [Requirement]
...

## Constraints
### C1: [Constraint]
**Source**: [Input name, location]
[Description and impact]

## Stakeholders
### S1: [Stakeholder/Role]
**Source**: [Input name, location]
**Interests**: [What they care about]

## Decisions Already Made
### D1: [Decision]
**Source**: [Input name, location]
**Rationale**: [Why this was decided]

## Contradictions & Ambiguities
### A1: [Issue]
**Sources**: [Conflicting inputs]
**Conflict**: [What contradicts]
**Impact**: [Why this matters]
**Resolution needed**: [Question for human]
```

### 5. Surface Questions

Add discovered questions to `08-OPEN-QUESTIONS.md`:

```markdown
## Question [N]: [Brief title]

**Discovered during**: Extraction from [input]
**Context**: [Full context for the question]
**Options** (if applicable):
- Option A: [Description]
- Option B: [Description]
**Impact**: [What this affects]
**Human response**: [To be filled]
```

### 6. Cross-Reference Check

Ensure all sources are attributed:
- Every extraction has source reference
- No orphaned items without attribution

### 7. Update OVERVIEW

Update `00-OVERVIEW.md`:
- Status: "Extracting" or "Extracted"
- Current phase information

### 8. Present Summary

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

## Large Input Handling

For inputs over 10000 lines:
- Process in chunks (e.g., 2000 lines at a time)
- Track progress: "Processing lines 1-2000 of 15000"
- Do NOT skip or summarize - full attention required
- May require multiple sessions

---

## Related Protocols

- Adding inputs → [add-input.md](add-input.md)
- Building concept → [conceptualize.md](conceptualize.md)
- Knowledge checkpoint → [../checkpoint.md](../checkpoint.md)
