# Anti-Patterns Reference

Common mistakes to avoid when using the workflow system.

---

## Document Management Anti-Patterns

### ❌ Creating Multiple Status Documents

**Wrong**:
```
work/001-feat-auth/
├── 00-OVERVIEW.md
├── status-update.md          ← DON'T
├── current-status.md         ← DON'T
└── summary-2025-01-15.md     ← DON'T
```

**Right**: Use only `00-OVERVIEW.md` as the single source of truth.

---

### ❌ Recreating Session Summaries

**Wrong**: Creating new summary files each session
```
session-1-summary.md
session-2-summary.md
session-3-summary.md
```

**Right**: Append to `03-PROGRESS-LOG.md`
```markdown
## 2025-01-15 Session 3

**Completed**:
- [x] Item 1
- [x] Item 2

**Next Session Start Here**:
Priority 1: [specific task]
```

---

### ❌ Documents Exceeding Max Length

**Wrong**: 10-page requirements document

**Right**: Split feature or move detail to knowledge docs

| Document | Max Length |
|----------|------------|
| OVERVIEW | 2 pages |
| REQUIREMENTS | 3 pages |
| IMPLEMENTATION-PLAN | 4 pages |
| TESTING-CHECKLIST | 2 pages |

---

### ❌ Duplicating Information

**Wrong**: Copying requirements into progress log, overview, and plan

**Right**: Reference other documents
```markdown
See requirements in 01-REQUIREMENTS.md section "Edge Cases"
```

---

## Session Management Anti-Patterns

### ❌ Starting Work Without Reading SSOT

**Wrong**:
```
Human: >>continue
Agent: [Immediately starts working without reading OVERVIEW]
```

**Right**:
```
Human: >>continue
Agent: [Reads 00-OVERVIEW.md, 03-PROGRESS-LOG.md, knowledge docs]
       Work: User Auth (feat)
       Status: In Progress
       Next: Implement login endpoint
       Ready to proceed?
```

---

### ❌ Vague Handoffs

**Wrong**:
```markdown
**Next**: Continue the feature
```

**Right**:
```markdown
**Next Session Start Here**:
Priority 1: Implement NotificationService.send() in src/services/notification.service.ts
Priority 2: Add tests for notification service
Files: src/services/notification.service.ts, src/tests/notification.test.ts
```

---

### ❌ Assuming Context from Previous Session

**Wrong**: Continuing work without re-reading state

**Right**: Always read SSOT at session start, even if you "remember"

---

### ❌ Making Major Changes Without Approval

**Wrong**:
```
[Refactors 5 files without asking]
```

**Right**:
```
I'll refactor these 5 files to implement the new strategy:
- file1.ts
- file2.ts
...

This affects [X functionality]. Proceed?
```

---

## Folder Structure Anti-Patterns

### ❌ Wrong Folder Numbering

**Wrong**:
```
work/
├── 001-feat-auth/
├── 001-maint-deps/    ← DUPLICATE NUMBER
└── 003-feat-api/
```

**Right**: Find highest number across ALL types, add 1
```
work/
├── 001-feat-auth/
├── 002-maint-deps/
└── 003-feat-api/
```

---

### ❌ Files in Wrong Locations

**Wrong**:
```
meta/
├── my-feature-notes.md    ← DON'T
└── templates/
```

**Right**: Work items in `work/`, knowledge in `knowledge/`

---

## Knowledge Anti-Patterns

### ❌ Skipping Knowledge Lookup

**Wrong**: Starting feature without checking knowledge base

**Right**: Always check at session start:
- `knowledge/SYSTEM-OVERVIEW.md`
- `knowledge/CONCEPTS-INDEX.md`
- Relevant `knowledge/subsystems/`

---

### ❌ Not Documenting Discoveries

**Wrong**: Learning important patterns but not recording them

**Right**: Update knowledge docs when you discover:
- Non-obvious patterns
- Gotchas worth noting
- Useful commands
- Subsystem insights

---

### ❌ Skipping Knowledge Checkpoint at Wrap

**Wrong**: `>>wrap` without updating knowledge

**Right**: At every `>>wrap`:
1. Did I discover patterns? → Update CONCEPTS-INDEX.md
2. Were there gotchas? → Update subsystem doc
3. Useful commands learned? → Update COMMANDS.md

---

## Concept Workflow Anti-Patterns

### ❌ Skipping Format Question for >>plan

**Wrong**:
```
Human: >>plan
Agent: [Generates work plan in arbitrary format]
```

**Right**:
```
Human: >>plan
Agent: What format would you like?
       - generic - Phases/Work Packages/Tasks
       - jira - Epics/Stories
       - github - Issues/Milestones
       - custom - Describe your structure
```

---

### ❌ Not Cascading Refinements

**Wrong**: Updating concept but not plan or roadmap

**Right**: `>>refine concept` must cascade:
```
concept → plan → roadmap
```

---

### ❌ Summarizing Large Inputs

**Wrong**: "This input is too long, I'll summarize..."

**Right**: Process large inputs in chunks with full attention
- Track progress: "Processing lines 1-2000 of 15000"
- Do NOT skip content

---

### ❌ More Than 7 Sub-Concepts

**Wrong**: Creating 12 sub-concepts

**Right**: Limit to 7, or suggest splitting:
```
Note: Identified 12 sub-concepts, but max is 7.
Suggest either:
1. Combine related concepts
2. Split into separate concept work items

Which approach?
```

---

## Success Indicators

You're following the protocol correctly if:

✅ Every session starts by reading SSOT
✅ Work items in numbered folders (001-TYPE-name)
✅ Progress log grows by appending
✅ Handoffs include specific next task with file path
✅ Documents stay within max length
✅ Human can resume work in < 2 minutes
✅ Knowledge updated when insights discovered
✅ Knowledge checkpoint done at >>wrap
✅ No duplicate summaries
