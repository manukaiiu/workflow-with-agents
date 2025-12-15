# Feedback: Workflow System Lost During Long Multi-Context Sessions

**ID**: FB-005
**Date**: 2025-12-10
**Source Project**: AID-CC Concept Work
**Category**: Agent Behavior / Context Management
**Priority**: High

---

## Observation

When the user said "wrap this up and create general information documents", the agent (me) provided a summary response but **failed to execute the `>>finalize` workflow protocol** defined in `ai-agent/meta/FOR-AGENTS.md`.

The user had to explicitly correct me:

> "if i am not mistaken, after reaching a final state of an initial phase like this, the agent workflow should guide the agent, in this case you, to create new folders for concept and workplan outside of work/nnn-... Including proper documentation."

## Root Cause Analysis

### 1. Context Window Exhaustion
The conversation spanned multiple context windows (conversation was summarized at least once). During summarization:
- **Preserved**: Task-specific details, file changes, user requests
- **Lost/Degraded**: Awareness of overarching workflow system in `FOR-AGENTS.md`

### 2. Workflow Instructions Not Re-Anchored
The `FOR-AGENTS.md` file was read at the start of the work session, but:
- Its content was not re-read after context summarization
- The `>>finalize` protocol was not included in the summarized context
- The agent proceeded based on immediate task context only

### 3. Natural Language Ambiguity
"Wrap up" was interpreted as:
- **Agent interpretation**: Provide a summary of what was done
- **User intent**: Execute finalization workflow (create folders, promote documents)

The agent defaulted to a conversational interpretation rather than checking workflow protocols.

### 4. Missing Trigger Recognition
The workflow defines `>>finalize` as a command trigger, but:
- User said "wrap up" (natural language equivalent)
- Agent did not recognize this as equivalent to `>>finalize`
- No mechanism prompted the agent to re-check workflow documents

## Impact

1. **User friction**: Required explicit correction
2. **Workflow bypass**: Finalization steps nearly skipped entirely
3. **Trust erosion**: User had to remind agent of its own workflow system
4. **Time waste**: Additional conversation round needed

## Suggested Solutions

### Option A: Explicit Workflow Anchoring in Summaries

When summarizing long conversations, ensure workflow context is preserved:

```markdown
## Workflow Context (from FOR-AGENTS.md)
- Current work type: concept
- Current phase: complete
- Available transitions: >>finalize, >>refine [phase]
- Finalization protocol: Create version folders, copy documents, create INPUTS-SUMMARY.md
```

**Pros**: Preserves workflow awareness across context boundaries
**Cons**: Consumes summary tokens, may not scale

### Option B: Trigger Word Recognition

Extend workflow system to recognize natural language equivalents:

| Protocol | Natural Language Triggers |
|----------|---------------------------|
| `>>finalize` | "wrap up", "complete", "finish", "done", "finalize" |
| `>>refine` | "improve", "iterate", "refine", "update" |
| `>>continue` | "resume", "keep going", "continue" |

When trigger words detected in user messages, agent should:
1. Identify potential workflow transition
2. Re-read relevant `FOR-AGENTS.md` section
3. Confirm with user if ambiguous

**Pros**: Natural interaction, doesn't require explicit commands
**Cons**: Risk of false positives, requires keyword maintenance

### Option C: Periodic Workflow Re-Anchoring

Add instruction to `FOR-AGENTS.md`:

> **Long Session Protocol**: If the conversation has been summarized (context window exceeded), re-read this file to refresh awareness of workflow protocols before responding to completion-related messages.

**Pros**: Simple instruction, agent-driven
**Cons**: Relies on agent recognizing summarization occurred

### Option D: End-of-Phase Checklist

Add explicit checklist to each work type template:

```markdown
## Phase Completion Checklist
Before marking any phase complete, verify:
- [ ] Have I checked FOR-AGENTS.md for phase transition protocols?
- [ ] Is there a finalization workflow I should execute?
- [ ] Have I created required output folders and documents?
```

**Pros**: Explicit reminder at critical points
**Cons**: Additional template complexity

## Recommendation

**Combination of Options B + C**:

1. Add natural language trigger recognition to workflow system
2. Add periodic re-anchoring instruction for long sessions
3. When user says completion-related words ("wrap up", "done", "finish"), agent should:
   - Recognize potential phase transition
   - Re-read `FOR-AGENTS.md` for applicable protocols
   - Execute workflow rather than just acknowledging

## Implementation Notes

For `FOR-AGENTS.md`, add section:

```markdown
## Natural Language Workflow Triggers

The following user phrases should trigger workflow protocol checks:

| User Says | Check Protocol |
|-----------|----------------|
| "wrap up", "wrap this up" | >>finalize |
| "we're done", "this is done" | >>finalize |
| "finish this", "complete this" | >>finalize |
| "let's refine", "needs improvement" | >>refine |
| "continue", "keep going" | >>continue |

When you detect these phrases:
1. Re-read the relevant workflow section
2. Execute the protocol steps
3. Do NOT just provide a summary response
```

---

## Meta

**Feedback Type**: Agent Behavior Improvement
**Affects**: `ai-agent/meta/FOR-AGENTS.md`
**Related Issues**: Context window summarization, workflow continuity
**Severity**: High - affects workflow completion reliability
