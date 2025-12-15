# Protocol: >>start

**Trigger**: `>>start [type] name` or "let's start a new..."
**Purpose**: Initialize new work item

---

## Syntax

```
>>start feat user-auth       # Feature
>>start maint deps-update    # Maintenance
>>start bug login-issue      # Bug fix
>>start concept platform     # Concept work
>>start my-feature           # Defaults to feat if type omitted
```

---

## Protocol Steps

### 1. Check Knowledge Base (Do First)

Read if they exist:
- `ai-agent/knowledge/SYSTEM-OVERVIEW.md`
- `ai-agent/knowledge/CONCEPTS-INDEX.md`
- `ai-agent/knowledge/COMMANDS.md`

Use this context to ask better questions.

### 2. Ensure Work Directory Exists

```bash
mkdir -p ai-agent/work
```

### 3. Determine Work Item Number

**Critical - follow exactly:**
1. List all folders in `ai-agent/work/`
2. Extract numeric prefix from each (e.g., `001` from `001-feat-auth`)
3. Find HIGHEST number across ALL folders
4. Next number = highest + 1
5. If no folders exist, start with `001`

**Example**: Folders `001-feat-auth`, `002-maint-deps` → next is `003`

### 4. Create Work Folder

Format: `ai-agent/work/NNN-TYPE-name/`
- 3-digit number (001, 002, etc.)
- Work type prefix (feat, maint, bug, concept)
- Kebab-case name

### 5. Copy Templates

**For `feat` (features)**:
- Copy from `meta/templates/features/`
- Set status "Planning", date

**For `maint` (maintenance)**:
- Copy from `meta/templates/maintenance/`
- Set status "Planning", date

**For `bug` (bugs)**:
- Copy from `meta/templates/features/`
- Set status "Investigating", date

**For `concept`**:
- Copy from `meta/templates/concept/`
- Create `01-INPUTS/` subfolder
- Set status "Gathering", date
- See [protocols/concept/gather.md](concept/gather.md) for full concept setup

### 6. Research and Document

If you research the codebase during planning:
- Update `knowledge/CONCEPTS-INDEX.md` with discovered patterns
- Create/update subsystem docs for significant findings
- Note in progress log: "Knowledge updated: [what]"

### 7. Present Questions

Ask clarifying questions informed by:
- Knowledge base research
- Template requirements
- Work type specifics

### 8. Wait for Answers

Don't proceed to implementation planning until human answers.

### 9. Update Work Index

If `ai-agent/work/WORK-INDEX.md` exists, add entry to "Active Work Items":

```markdown
| NNN | TYPE | name | Planning | - | YYYY-MM-DD |
```

If it doesn't exist, create from template `meta/templates/WORK-INDEX.md`.

---

## Response Template

```
I'll create the foundation for [TYPE]: [name].

Created work folder: ai-agent/work/NNN-TYPE-name/

Created:
- 00-OVERVIEW.md (draft)
- 01-REQUIREMENTS.md / 01-SCOPE.md (draft)
[- 01-INPUTS/INDEX.md (for concept)]

[If knowledge updated:]
Updated knowledge:
- CONCEPTS-INDEX.md: Added [pattern/concept]

Questions about [requirements/scope]:
1. [Question 1]
2. [Question 2]
3. [Question 3]

Please answer these so I can create an implementation plan.
```

---

## After Human Answers

1. Create `02-IMPLEMENTATION-PLAN.md`
2. Present plan for approval
3. Wait for "approved" before implementing

---

## Related Protocols

- Concept work setup → [protocols/concept/gather.md](concept/gather.md)
- Continuing work → [protocols/continue.md](continue.md)
- Knowledge setup → [protocols/init-knowledge.md](init-knowledge.md)
