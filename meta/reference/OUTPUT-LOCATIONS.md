# Output Location Guidelines

When and where to create/edit files during work.

---

## The Two Modes

### 1. Work Item Mode (Default)

When a work item exists in `work/NNN-TYPE-name/`:
- All work happens within that folder
- Outputs go to `90-OUTPUTS/` subfolder
- Finalization promotes to top-level folders
- Progress tracked in work item docs

**This is the preferred mode** - it provides:
- Traceability
- Version control
- Clear workflow stages
- Easy rollback

### 2. Direct Edit Mode (Exception)

When user explicitly requests edits to files outside work items:
- User specifies exact location
- Agent confirms before proceeding
- No work item tracking

**Use sparingly** - appropriate for:
- Quick fixes to existing files
- Updates unrelated to any work item
- Explicit user override

---

## Decision Tree

```
User requests file creation/edit
          │
          ▼
┌─────────────────────────┐
│ Is there an active      │
│ work item for this?     │
└─────────────────────────┘
          │
    ┌─────┴─────┐
    │           │
   YES          NO
    │           │
    ▼           ▼
┌─────────┐  ┌─────────────────┐
│ Work in │  │ Ask user:       │
│ work/   │  │ - Create work   │
│ folder  │  │   item? (>>start)│
└─────────┘  │ - Or direct     │
             │   edit? (confirm │
             │   location)      │
             └─────────────────┘
```

---

## Location Matrix

| File Type | During Work | After Finalize | Direct Edit OK? |
|-----------|-------------|----------------|-----------------|
| Concept drafts | `work/NNN/03-CONCEPT*.md` | `concepts/name/vN/` | Ask first |
| Work plans | `work/NNN/04-WORKPLAN.md` | `workplans/name/vN/` | Ask first |
| Roadmaps | `work/NNN/05-ROADMAP*.md` | `workplans/name/vN/` | Ask first |
| Deliverables | `work/NNN/90-OUTPUTS/` | User decides | Yes, with confirmation |
| Knowledge docs | `knowledge/` | N/A | Yes |
| Project code | Project folders | N/A | Yes, per requirements |

---

## Protecting Finalized Outputs

Files in `concepts/` and `workplans/` are **finalized artifacts**.

When user requests changes to finalized files:

1. **Ask clarifying questions**:
   ```
   This file is in concepts/[name]/v1/ (finalized output).

   Options:
   1. Edit in place (modifies finalized version)
   2. Create new version (>>new-version)
   3. Create new work item to iterate

   Which approach?
   ```

2. **If editing in place**: Confirm user understands this modifies the "official" version

3. **For significant changes**: Recommend `>>new-version` to preserve history

---

## Red Flags to Watch For

**Pause and confirm** when:

- Creating files outside `work/` or `knowledge/` without explicit path
- User says "update the concept" but there's an active work item
- Request implies bypassing finalization workflow
- Editing finalized outputs without clear intent

**Example confirmations**:

```
"You mentioned updating the roadmap. Should I:
1. Edit the draft in work/003-concept-platform/05-ROADMAP.md
2. Edit the finalized version in workplans/platform/v1/ROADMAP.md
3. Create a new version (v2)?"
```

```
"I'll create this deliverable in work/003-concept-platform/90-OUTPUTS/.
Is that the right location, or did you want it somewhere else?"
```

---

## Summary

| Principle | Implementation |
|-----------|----------------|
| Default to work items | Create outputs in `work/` folder |
| Controlled promotion | Use `>>finalize` to move to top-level |
| Protect finalized work | Ask before editing `concepts/` or `workplans/` |
| Confirm when uncertain | Ask about location for anything unusual |
| Track everything | Work items provide traceability |
