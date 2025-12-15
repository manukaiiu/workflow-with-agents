# Protocol: >>new-version

**Trigger**: `>>new-version` or "let's create a new version", "major revision needed"
**Purpose**: Create new version for major concept revision

---

## When to Use

Use `>>new-version` when:
- Weeks have passed with significant changes
- New major inputs (meetings, discoveries)
- Fundamental direction change
- Previous version finalized, need fresh iteration

Do NOT use when:
- Minor updates (use `>>refine` instead)
- Fixing errors (use `>>refine` instead)
- Still in initial development

---

## Protocol Steps

### 1. Determine New Version Number

Check existing versions:
- `ai-agent/concepts/[name]/v1/` exists → new version is v2
- `ai-agent/concepts/[name]/v2/` exists → new version is v3
- etc.

### 2. Determine Work Item Number

Follow standard numbering:
- List all folders in `ai-agent/work/`
- Find highest number
- Next number = highest + 1

### 3. Create New Work Folder

```bash
ai-agent/work/NNN-concept-name-v2/
```

### 4. Copy Current State

Copy from either:
- Previous finalized version (`concepts/[name]/vN/`)
- Or current working folder if not finalized

Files to copy:
- 03-CONCEPT.md and sub-concepts
- 04-WORKPLAN.md
- 05-ROADMAP.md

### 5. Initialize New Version

Create fresh:
- `00-OVERVIEW.md` with reference to previous version
- `01-INPUTS/INDEX.md` (empty or with carried-over inputs)
- `07-REFINEMENT-LOG.md` (fresh)
- `08-OPEN-QUESTIONS.md` (fresh)

### 6. Update OVERVIEW for New Version

```markdown
# Concept Overview: [Name] v2

**Type**: Concept
**Status**: Gathering
**Created**: YYYY-MM-DD
**Previous Version**: v1 (ai-agent/concepts/[name]/v1/)

## Version Notes
This version builds on v1 with the following major changes:
- [Change 1]
- [Change 2]

## Quick Context
[Updated description]

## Current Phase
Gathering - Collecting new inputs for v2

## What's New in v2
- [New input 1]
- [New consideration]
```

### 7. Confirm to Human

```
Creating new version for concept: [name]

Created: ai-agent/work/NNN-concept-name-v2/
- Copied current state as starting point
- Fresh refinement log
- Reference to v1 in overview

Ready to:
- >>add-input [new inputs]
- >>refine [phase] for updates
- >>continue with changes

What new inputs or changes should we process?
```

---

## Version Relationship

Each version should be:
- **Self-contained**: Can be understood without previous versions
- **Referenced**: Links to previous version for history
- **Independent**: Changes don't affect finalized versions

---

## When to Finalize vs New Version

| Scenario | Action |
|----------|--------|
| Still developing, need changes | `>>refine` |
| Ready for use, may update later | `>>finalize` |
| Finalized, need major revision | `>>new-version` |
| Finalized, need minor fix | `>>refine` then `>>finalize` again |

---

## Related Protocols

- Refinement → [refine.md](refine.md)
- Finalizing → [finalize.md](finalize.md)
- Starting concept → [start-concept.md](start-concept.md)
