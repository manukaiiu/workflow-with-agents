# Protocol: >>start concept

**Trigger**: `>>start concept <name>` or "let's start a new concept"
**Purpose**: Initialize new concept work item

---

## Protocol Steps

### 1. Check Knowledge Base

Read existing knowledge:
- `ai-agent/knowledge/SYSTEM-OVERVIEW.md` for project context
- `ai-agent/knowledge/CONCEPTS-INDEX.md` for relevant patterns
- Relevant subsystem notes in `knowledge/subsystems/`

### 2. Ensure Directories Exist

```bash
mkdir -p ai-agent/work
```

### 3. Determine Work Item Number

Follow standard numbering:
- List all folders in `ai-agent/work/`
- Find HIGHEST number across ALL folders
- Next number = highest + 1
- If no folders exist, start with 001

### 4. Create Concept Work Folder

```bash
ai-agent/work/NNN-concept-name/
├── 01-INPUTS/
```

### 5. Copy and Customize Templates

From `meta/templates/concept/`:
- `00-OVERVIEW.md`: Set name, status "Gathering", date
- `01-INPUTS/INDEX.md`: Empty inventory ready for inputs
- `08-OPEN-QUESTIONS.md`: Template ready for questions

### 6. Ask About Input Sources

```
I'll create the foundation for concept: [name].

Created work folder: ai-agent/work/NNN-concept-name/

Created:
- 00-OVERVIEW.md (status: Gathering)
- 01-INPUTS/INDEX.md (empty)
- 08-OPEN-QUESTIONS.md (ready)

Questions about inputs:
1. What raw inputs will we analyze? (conversations, documents, PDFs?)
2. Are there URLs to fetch or files to add?
3. Any specific areas to focus on?

Use >>add-input [path/url] to add input sources.
```

---

## Concept OVERVIEW Template

```markdown
# Concept Overview: [Name]

**Type**: Concept
**Status**: Gathering
**Created**: YYYY-MM-DD

## Quick Context
[Brief description of what this concept work will produce]

## Current Phase
Gathering - Collecting inputs for analysis

## Inputs
- [ ] [Expected input 1]
- [ ] [Expected input 2]

## Open Questions
See 08-OPEN-QUESTIONS.md

## File Index
| File | Type | Purpose |
|------|------|---------|
| 00-OVERVIEW.md | Core | This file - status and navigation |
| 01-INPUTS/INDEX.md | Core | Input inventory |
| 08-OPEN-QUESTIONS.md | Core | Questions for human |
```

---

## Next Steps

After creating concept work item:
1. Add inputs with `>>add-input [path/url]`
2. When inputs complete, use `>>extract` to process
3. Follow concept workflow phases

---

## Related Protocols

- Adding inputs → [add-input.md](add-input.md)
- Extracting from inputs → [extract.md](extract.md)
- Concept workflow overview → [overview.md](overview.md)
