# Feedback: Human-Agent Ping-Pong Documentation

**ID**: FB-007
**Date**: 2025-12-11
**Source Project**: WP4 Expert Involvement Process (002-concept-expert-involvement)
**Category**: Workflow System / Human-Agent Collaboration
**Priority**: High

---

## Observation

During work items, there's a recurring pattern:
1. Agent produces output (concept, deliverable, question)
2. Human reviews and responds with remarks, answers, decisions
3. Human's response needs to go somewhere appropriate
4. Human either:
   - Writes in a text file and points agent to it (extra effort)
   - Pastes directly into prompt (lost for future documentation)
   - Edits the document directly (works but informal)

**Problem**: Human feedback is valuable context that often gets lost or requires awkward workarounds to preserve.

**Example from this work item**:
- Human responses were added inline to `03-CONCEPT.md` under "Human response" and "Answers by Human"
- This worked but felt ad-hoc
- Future agents or humans reviewing the work item don't have a clear trail of decisions

---

## Current Workarounds

| Approach | Pros | Cons |
|----------|------|------|
| Edit document directly | Quick, in context | Clutters final document |
| Separate response file | Clean separation | Extra file to manage, agent must be pointed to it |
| Paste in prompt | Immediate | Lost after session, no documentation |
| Comment in conversation | Agent sees it | Not persisted in work item |

---

## Suggested Solutions

### Option A: Dedicated Feedback Log

Add a standard document to work items for human-agent dialogue:

**`06-DIALOGUE.md`** (or `FEEDBACK-LOG.md`)

```markdown
# Human-Agent Dialogue Log

## Entry 1: [Date/Time or Phase]
**Context**: [What agent produced]
**Human Feedback**:
> [Human's remarks, decisions, answers]

**Agent Response**: [How agent incorporated feedback]
**Outcome**: [What changed]

---

## Entry 2: ...
```

**Pros**:
- Clear audit trail of decisions
- Structured place for feedback
- Preserves context for future sessions

**Cons**:
- Another file to maintain
- May feel bureaucratic for quick exchanges

### Option B: Inline Feedback Blocks

Define a convention for inline feedback in any document:

```markdown
<!-- HUMAN-FEEDBACK: 2025-12-11
Your remarks here...
-->

<!-- AGENT-RESPONSE: 2025-12-11
How feedback was incorporated...
-->
```

**Pros**:
- Feedback stays with relevant content
- No extra files
- Can be stripped for final versions

**Cons**:
- Clutters documents
- Harder to see all feedback at once

### Option C: Conversation Summary Section in OVERVIEW

Add a "Decision Log" section to 00-OVERVIEW.md:

```markdown
## Decision Log

| Date | Topic | Human Input | Resolution |
|------|-------|-------------|------------|
| 2025-12-11 | Question framework weight | "Can be lighter" | Kept minimal |
| 2025-12-11 | Expert package approach | "Use report itself" | Refined to cover letter + reading guide |
```

**Pros**:
- Centralized in existing file
- Quick to scan
- Links to decisions

**Cons**:
- May not capture full context
- Table format limits detail

### Option D: Hybrid Approach (Recommended)

Combine approaches based on feedback type:

| Feedback Type | Where to Capture |
|---------------|------------------|
| **Quick decisions** | Decision Log table in 00-OVERVIEW.md |
| **Detailed remarks** | Inline in relevant document with `<!-- HUMAN-FEEDBACK -->` |
| **Multi-topic responses** | Dedicated entry in 06-DIALOGUE.md |
| **Corrections/refinements** | Direct edit + note in Decision Log |

**Workflow prompt for agent**:
> "When you present options or questions, explicitly ask: 'Where would you like to record your response?' Options: (1) I'll update the document, (2) Add to Decision Log, (3) Create dialogue entry"

---

## Implementation Suggestions

### For FOR-AGENTS.md

Add section on human feedback capture:

```markdown
## Capturing Human Feedback

Human responses during work items are valuable and should be preserved.

**Decision Log** (in 00-OVERVIEW.md):
For quick decisions, add to the Decision Log table:
| Date | Topic | Human Input | Resolution |

**Inline Feedback** (in any document):
For detailed remarks on specific content:
<!-- HUMAN-FEEDBACK: [date]
[feedback content]
-->

**Dialogue Log** (06-DIALOGUE.md):
For complex multi-topic responses, create dedicated entries.

**Agent responsibility**:
- When presenting options, offer to capture the response
- After receiving feedback, confirm where it was recorded
- Summarize key decisions in 00-OVERVIEW.md Decision Log
```

### For Templates

Add to `00-OVERVIEW.md` template:

```markdown
## Decision Log

| Date | Topic | Human Input | Resolution |
|------|-------|-------------|------------|
| | | | |
```

Add optional `06-DIALOGUE.md` template:

```markdown
# Human-Agent Dialogue Log

**Work Item**: [Name]
**Purpose**: Captures significant human-agent exchanges for documentation and future reference.

---

## [Date]: [Topic]

**Context**: [What prompted feedback]

**Human**:
> [Feedback]

**Agent**: [Response/incorporation]

**Outcome**: [Resolution]

---
```

---

## Benefits

1. **Audit trail** - Decisions are documented and traceable
2. **Context preservation** - Future sessions/agents understand why choices were made
3. **Reduced friction** - Human knows where to put feedback
4. **Quality documentation** - Work items tell the full story

---

## Related

- **FB-005**: Workflow loss in long sessions (context gets summarized)
- **FB-006**: Process work type (different documentation needs)
- This feedback: Human input capture

Together these suggest the workflow needs better support for the collaborative, iterative nature of human-agent work.

---

## Meta

**Feedback Type**: Workflow System Enhancement
**Affects**: `ai-agent/meta/FOR-AGENTS.md`, templates
**Severity**: High - affects every work item
