# Protocol: >>refine

**Trigger**: `>>refine <phase>` or "let's update the [phase]", "need to change..."
**Purpose**: Enter refinement cycle at specified phase

---

## Syntax

```
>>refine extract
>>refine concept
>>refine plan
>>refine roadmap
```

---

## Protocol Steps

### 1. Log Refinement Start

Create entry in `07-REFINEMENT-LOG.md`:

```markdown
## Refinement Cycle [N]

**Date**: [date]
**Entry Point**: [phase]
**Trigger**: Human request | Agent detection
**Reason**: [Why refinement needed]
**Version**: [current version → new version]

### Changes Made
[To be filled as changes happen]

### Cross-Reference Updates
- [ ] Updated traceability in [doc]
- [ ] Updated source references in [doc]
```

### 2. Apply Changes to Entry Phase

Make the requested changes at the specified phase:

| Entry Point | Document(s) to Update |
|-------------|----------------------|
| extract | 02-EXTRACTIONS.md |
| concept | 03-CONCEPT.md, sub-concepts |
| plan | 04-WORKPLAN.md |
| roadmap | 05-ROADMAP.md, mermaid |

### 3. Cascade Forward (CRITICAL)

Changes MUST propagate to downstream documents:

```
extract → concept → plan → roadmap
concept → plan → roadmap
plan → roadmap
roadmap → only roadmap
```

For each downstream phase:
1. Review impact of changes
2. Update affected elements
3. Maintain traceability links
4. Document what changed

### 4. Update ALL Cross-References

Ensure consistency:
- Extraction IDs still valid
- Concept references correct
- Work plan traces to concept
- Roadmap reflects plan

### 5. Update OVERVIEW

Update `00-OVERVIEW.md`:
- Note refinement cycle
- Update any status changes

### 6. Complete Refinement Log

```markdown
### Changes Made
- [Phase]: [Specific changes]
- [Cascaded phase]: [What was updated]
- [Cascaded phase]: [What was updated]

### Cross-Reference Updates
- [x] Updated traceability in 03-CONCEPT.md
- [x] Updated source references in 04-WORKPLAN.md
- [x] Updated dependencies in 05-ROADMAP.md
```

### 7. Notify Human

```
Refinement cycle [N] started at [phase].

Changes made:
- [Phase]: [Changes]

Cascaded to:
- [Next phase]: [Changes]
- [Next phase]: [Changes]

Cross-references updated:
- [List of documents]

Updated: 07-REFINEMENT-LOG.md

Refinement complete. Ready to continue.
```

---

## Proactive Refinement Detection

Agent should SUGGEST refinement when detecting:
- Inconsistencies between documents
- New information contradicting existing content
- Gaps in traceability
- Scope changes implied by recent inputs

```
I've noticed [inconsistency/gap].

This affects:
- [Document 1]: [How]
- [Document 2]: [How]

Suggest: >>refine [phase] to address this.

Should I proceed with refinement?
```

---

## Refinement Log Template

```markdown
# Refinement Log

**Concept**: [Name]

## Refinement Cycle 1

**Date**: 2025-01-15
**Entry Point**: concept
**Trigger**: Human request
**Reason**: Scope adjustment - adding mobile support
**Version**: 1.0 → 1.1

### Changes Made
- 03-CONCEPT.md: Added mobile sub-concept, updated scope table
- 04-WORKPLAN.md: Added 2 new work packages for mobile
- 05-ROADMAP.md: Extended Wave 3, added mobile milestone

### Cross-Reference Updates
- [x] Added R8 (mobile requirement) to extractions
- [x] Linked new concept elements to R8
- [x] Updated traceability matrix
- [x] Updated dependency graph
```

---

## Related Protocols

- Extracting → [extract.md](extract.md)
- Conceptualizing → [conceptualize.md](conceptualize.md)
- Planning → [plan.md](plan.md)
- Roadmapping → [roadmap.md](roadmap.md)
