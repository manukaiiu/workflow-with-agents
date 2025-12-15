# Feedback: Tracking Questions for Human Consortium Discussion

**ID**: FB-004
**Date**: 2025-12-09
**Source Project**: AID-CC Concept Work
**Category**: Workflow Design / Output Types
**Priority**: Medium
**Related**: FB-003

---

## Observation

During concept work, several questions emerged that:
1. Could not be answered by the AI agent
2. Required human-to-human discussion with consortium partners
3. Needed to be tracked for follow-up in appropriate meetings

The human collaborator specifically requested: "For this it would be interesting to have some document with the questions me as the human should discuss with the other humans in the project."

## Current Handling

Questions were placed in:
- `08-OPEN-QUESTIONS.md` under "Questions for Consortium Discussion"
- Individual concept documents under "Questions for Consortium Discussion" sections

This works but is scattered and informal.

## The Pattern

**Agent-generated questions for human discussion** are a distinct output type:
- They're not "open questions" (blocking the agent)
- They're not "tasks" (agent can't execute them)
- They're "discussion items" for the human to take to meetings

## Suggested Solution

### Option A: Dedicated Section in Open Questions

Keep the current approach but formalize it:
```markdown
## Open Questions (Blocking Agent)
[Questions the agent needs answered to proceed]

## Discussion Items (For Human Meetings)
[Questions for the human to discuss with consortium]
```

### Option B: Separate Document Type

Create a new document type in concept work:
```
ai-agent/work/[concept]/
├── ...
├── 08-OPEN-QUESTIONS.md        # Agent-blocking questions
└── 09-DISCUSSION-ITEMS.md      # Human meeting preparation
```

Structure for discussion items:
```markdown
# Discussion Items for [Project]

## For Meeting: [Meeting Type]
| # | Topic | Context | Decision Needed |
|---|-------|---------|-----------------|
| 1 | OAuth provider | Auth design depends on this | Which OAuth provider? |

## Action Items from Discussions
| Meeting | Date | Decision | Impact |
|---------|------|----------|--------|
```

### Option C: Checklist in Overview

Add a "Human Action Items" section to `00-OVERVIEW.md`:
```markdown
## Human Action Items

These items require human-to-human discussion:

### For Next WP3 Meeting
- [ ] Confirm deployment architecture
- [ ] Review OAuth approach

### For Next WP5 Meeting
- [ ] Orchestra sandbox access
```

## Recommendation

**Option B** (Separate Document) is cleanest for complex projects:
- Clear separation of concerns
- Can be exported/printed for meetings
- Tracks decisions made
- Doesn't clutter open questions

For simpler projects, **Option C** (checklist in overview) may suffice.

## Template Suggestion

Add to concept templates:
```markdown
# Discussion Items: [Concept Name]

**Last Updated**: [YYYY-MM-DD]
**Items Pending**: [N]
**Items Resolved**: [N]

---

## Pending Discussion Items

### Meeting Type: [WP3 Technical / Consortium / etc.]

| ID | Topic | Context | Question for Discussion |
|----|-------|---------|------------------------|
| DI-1 | [Topic] | [Why it matters] | [Specific question] |

---

## Resolved Items

| ID | Topic | Meeting | Date | Decision | Impact on Concept |
|----|-------|---------|------|----------|-------------------|
| DI-1 | [Topic] | [Which meeting] | [Date] | [What was decided] | [How concept was updated] |
```

---

## Meta

**Feedback Type**: Output Type Definition
**Affects**: Concept templates, FOR-AGENTS.md
**Pattern**: "Questions for human discussion" as distinct from "questions blocking agent"
