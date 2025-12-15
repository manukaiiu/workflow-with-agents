# Feedback: Output File Organization in Work Items

**ID**: FB-008
**Date**: 2025-12-11
**Source Project**: WP4 Expert Involvement Process (002-concept-expert-involvement)
**Category**: Workflow System / File Organization
**Priority**: Medium

---

## Observation

Work items generate additional documents beyond the predefined templates. In work item 002:

**Template files** (expected):
- `00-OVERVIEW.md`
- `01-INPUTS/INDEX.md`
- `03-CONCEPT.md`

**Additional files** (created ad-hoc):
- `03-DELIVERABLES/question-collection-template.md`
- `03-DELIVERABLES/expert-package-refined.md`
- `03-DELIVERABLES/bridging-input-framing-chapters.md`
- `03-DELIVERABLES/work-sequence-and-dependencies.md`

**Problem**:
- Additional files "flood" the work item folder
- No clear convention for numbering/naming
- Hard to grasp what exists at a glance
- Future template improvements might conflict with existing numbering

---

## Current State

Work item 002 ended up with:
```
002-concept-expert-involvement/
├── 00-OVERVIEW.md
├── 01-INPUTS/
│   └── INDEX.md
├── 03-CONCEPT.md
└── 03-DELIVERABLES/
    ├── question-collection-template.md
    ├── expert-package-refined.md
    ├── bridging-input-framing-chapters.md
    └── work-sequence-and-dependencies.md
```

The `03-DELIVERABLES/` folder was created ad-hoc to contain outputs.

---

## Suggested Solutions

### Solution 1: Reserved Numbering + High Start for Work-Item Specific

Reserve low numbers (00-09) for template files, start work-item specific at 10+:

```
Template files (reserved 00-09):
  00-OVERVIEW.md
  01-INPUTS/
  02-EXTRACTIONS.md (if used)
  03-CONCEPT.md
  04-WORKPLAN.md (if used)
  05-ROADMAP.md (if used)
  06-DIALOGUE.md (if used, per FB-007)
  07-[reserved]
  08-OPEN-QUESTIONS.md
  09-[reserved]

Work-item specific (10+):
  10-deliverable-name.md
  11-another-output.md
  12-SUBFOLDER/
      └── contents...
```

**Pros**: Clear separation, room for template growth
**Cons**: Higher numbers feel arbitrary

### Solution 2: Dedicated Output Folder with Index

Standardize an output folder in templates:

```
XX-concept-name/
├── 00-OVERVIEW.md
├── 01-INPUTS/
├── 03-CONCEPT.md
└── 90-OUTPUTS/          ← Standard folder for deliverables
    ├── INDEX.md         ← Lists all outputs
    ├── template-x.md
    └── document-y.md
```

**Pros**:
- Clean separation
- INDEX.md provides table of contents
- `90-` ensures it sorts to end

**Cons**: Extra nesting level

### Solution 3: Table of Contents in 00-OVERVIEW.md (Recommended)

Add a comprehensive file listing to 00-OVERVIEW.md:

```markdown
## File Index

| File | Type | Purpose |
|------|------|---------|
| 00-OVERVIEW.md | Template | Status and navigation (this file) |
| 01-INPUTS/INDEX.md | Template | Input sources |
| 03-CONCEPT.md | Template | Main concept document |
| 03-DELIVERABLES/ | Ad-hoc | Output folder |
| ├─ question-collection-template.md | Deliverable | MS Word template |
| ├─ expert-package-refined.md | Deliverable | Expert package design |
| ├─ bridging-input-framing-chapters.md | Bridging | Input for next work item |
| └─ work-sequence-and-dependencies.md | Reference | Work item sequencing |
```

**Pros**:
- Easy to grasp at a glance
- No structural changes needed
- Agent can maintain it
- Shows purpose of each file

**Cons**:
- Requires maintenance
- Can get out of sync

### Solution 4: Hybrid (Recommended)

Combine solutions 2 and 3:

1. **Standard output folder**: `90-OUTPUTS/` for deliverables
2. **File Index in OVERVIEW**: Always maintain a table of contents
3. **Naming convention**: Deliverables use descriptive names (no numbers)

```
XX-concept-name/
├── 00-OVERVIEW.md           ← Contains File Index table
├── 01-INPUTS/
├── 03-CONCEPT.md
├── 06-DIALOGUE.md           ← If needed (per FB-007)
└── 90-OUTPUTS/
    ├── template-name.md
    ├── strategy-name.md
    └── bridging-name.md
```

---

## Implementation

### For 00-OVERVIEW.md Template

Add File Index section:

```markdown
## File Index

| File | Type | Purpose |
|------|------|---------|
| 00-OVERVIEW.md | Core | Status and navigation |
| 01-INPUTS/INDEX.md | Core | Input inventory |
| 03-CONCEPT.md | Core | Main concept |
| 90-OUTPUTS/ | Outputs | Work item deliverables |

*Agent: Update this table when creating new files*
```

### For FOR-AGENTS.md

Add file organization guidance:

```markdown
## File Organization in Work Items

**Template files** (00-09): Core workflow documents
- Always present or explicitly skipped
- Numbered per template

**Dialogue/Feedback** (06): Human-agent exchanges
- Created when needed

**Outputs** (90-OUTPUTS/): Work item deliverables
- Templates, documents, artifacts produced
- Use descriptive names (no numbers)
- Update File Index in 00-OVERVIEW.md

**Maintenance**:
- When creating new files, add to File Index
- When deleting files, remove from File Index
```

---

## Benefits

1. **Discoverability** - File Index shows what exists
2. **Scalability** - Template can grow (reserved 00-09)
3. **Clarity** - Outputs separated from workflow docs
4. **Maintenance** - Agent can keep index updated

---

## Meta

**Feedback Type**: Workflow System Enhancement
**Affects**: `ai-agent/meta/FOR-AGENTS.md`, templates
**Related**: FB-006 (process work type), FB-007 (dialogue capture)
**Severity**: Medium - organizational friction
