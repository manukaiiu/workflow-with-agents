# Protocol: >>finalize

**Trigger**: `>>finalize` or "let's finalize this concept", "we're done"
**Purpose**: Complete concept work and promote to top-level folders

---

## Protocol Steps

### 1. Verify Completeness

Check all requirements:

```
Verifying completeness...
```

| Check | Document | Requirement |
|-------|----------|-------------|
| ✓/❌ | 01-INPUTS/INDEX.md | All inputs `[x] Extracted` |
| ✓/❌ | 08-OPEN-QUESTIONS.md | No unresolved questions |
| ✓/❌ | 03-CONCEPT.md | Complete and reviewed |
| ✓/❌ | 04-WORKPLAN.md | Complete and reviewed |
| ✓/❌ | 05-ROADMAP.md | Complete and reviewed |

If incomplete:
```
Cannot finalize - work not complete:
❌ [List incomplete items]

Complete these first, then use >>finalize
```

### 2. Determine Version

Check if concept already exists:
- Look for `ai-agent/concepts/[name]/`
- If new: create `v1/`
- If exists: create next version `vN/`

### 3. Create Finalized Folders

```bash
mkdir -p ai-agent/concepts/[name]/vN/
mkdir -p ai-agent/workplans/[name]/vN/
```

### 4. Copy Finalized Documents

**To concepts/[name]/vN/**:
- `CONCEPT.md` (from 03-CONCEPT.md)
- `CONCEPT-[sub].md` (all sub-concepts)
- `INPUTS-SUMMARY.md` (generated from INDEX.md)

**To workplans/[name]/vN/**:
- `WORKPLAN.md` (from 04-WORKPLAN.md)
- `ROADMAP.md` (from 05-ROADMAP.md)
- `ROADMAP.mermaid.md` (from 05-ROADMAP.mermaid.md)

### 5. Create INPUTS-SUMMARY.md

```markdown
# Inputs Summary: [Name]

**Finalized**: [Date]
**Version**: [vN]
**Source Work Item**: NNN-concept-name

## Inputs Processed

| Input | Type | Key Contributions |
|-------|------|-------------------|
| [Name] | [Type] | [What it contributed] |

## Extraction Statistics
- Themes: [N]
- Requirements: [N]
- Constraints: [N]
- Decisions: [N]

## Source Reference
Full extraction details available in archived work item.
```

### 6. Update Working Folder

Update `00-OVERVIEW.md`:
- Status: "Finalized"
- Finalized: [date]
- Output locations: [paths]

### 7. Ask About Archive

```
Verifying completeness...
✓ All inputs processed
✓ No unresolved questions
✓ Concept complete
✓ Work plan complete
✓ Roadmap complete

Finalizing...

Created:
- ai-agent/concepts/[name]/v1/
  - CONCEPT.md
  - CONCEPT-[sub].md (x[N])
  - INPUTS-SUMMARY.md
- ai-agent/workplans/[name]/v1/
  - WORKPLAN.md
  - ROADMAP.md
  - ROADMAP.mermaid.md

Updated: 00-OVERVIEW.md (status: Finalized)

Concept work complete! 🎉

Archive the working folder? (y/n)
- Yes: Move to ai-agent/work/archive/
- No: Keep in ai-agent/work/ for reference
```

---

## Version History

When creating subsequent versions:
- Reference previous version in new CONCEPT.md
- Note what changed from previous version
- Keep versions independent (can be understood alone)

---

## Finalized Folder Structure

```
ai-agent/
├── concepts/
│   └── [name]/
│       ├── v1/
│       │   ├── CONCEPT.md
│       │   ├── CONCEPT-auth.md
│       │   ├── CONCEPT-data.md
│       │   └── INPUTS-SUMMARY.md
│       └── v2/
│           └── [same structure]
├── workplans/
│   └── [name]/
│       ├── v1/
│       │   ├── WORKPLAN.md
│       │   ├── ROADMAP.md
│       │   └── ROADMAP.mermaid.md
│       └── v2/
│           └── [same structure]
```

---

## Related Protocols

- Creating new version → [new-version.md](new-version.md)
- Roadmapping → [roadmap.md](roadmap.md)
- Archiving → [../archive.md](../archive.md)
