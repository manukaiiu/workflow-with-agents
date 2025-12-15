# Workflow System Glossary

Quick reference for terms and abbreviations used in the workflow system.

---

## Core Terms

| Term | Definition |
|------|------------|
| **SSOT** | Single Source of Truth - `00-OVERVIEW.md` in each work item |
| **Work Item** | A tracked unit of work (feature, bug, maintenance, concept) |
| **Knowledge Base** | `ai-agent/knowledge/` folder with project documentation |
| **Protocol** | A defined procedure triggered by `>>` commands |

---

## Work Types

| Type | Prefix | Description |
|------|--------|-------------|
| **Feature** | `feat` | New functionality or enhancements |
| **Bug** | `bug` | Bug fixes |
| **Maintenance** | `maint` | Dependency updates, refactoring, security, builds |
| **Concept** | `concept` | Complex conceptualization with work plans and roadmaps |

---

## Document Abbreviations

| Document | Purpose |
|----------|---------|
| `00-OVERVIEW` | Status, navigation, quick context (SSOT) |
| `01-REQUIREMENTS` | What to build (features/bugs) |
| `01-SCOPE` | What's included (maintenance) |
| `01-INPUTS/INDEX` | Input inventory (concepts) |
| `02-IMPLEMENTATION-PLAN` | How to build, phases |
| `02-EXTRACTIONS` | Extracted info from inputs (concepts) |
| `03-PROGRESS-LOG` | Append-only session log |
| `03-CONCEPT` | Main concept document |
| `04-TESTING-CHECKLIST` | Test scenarios |
| `04-WORKPLAN` | Work breakdown (concepts) |
| `05-ROADMAP` | Sequencing and dependencies (concepts) |

---

## Extraction IDs (Concept Workflow)

| Prefix | Category |
|--------|----------|
| **T** | Themes & Patterns (T1, T2...) |
| **R** | Requirements (R1, R2...) |
| **C** | Constraints (C1, C2...) |
| **S** | Stakeholders (S1, S2...) |
| **D** | Decisions Already Made (D1, D2...) |
| **A** | Ambiguities/Contradictions (A1, A2...) |

---

## Status Indicators

| Symbol | Meaning |
|--------|---------|
| `[ ]` | Not started / Not checked |
| `[x]` | Complete / Checked |
| `[~]` | In progress |
| `[P]` | Paused |
| `✓` | Done (in summaries) |
| `~` | In progress (in summaries) |
| `-` | Pending (in summaries) |
| `❌` | Blocked or failed |

---

## Work Item Statuses

| Status | Meaning |
|--------|---------|
| **Planning** | Gathering requirements, asking questions |
| **In Progress** | Active development |
| **Testing** | Running tests, verifying |
| **Review** | Awaiting human review |
| **Paused** | Interrupted, context captured |
| **Complete** | All done, ready for archive |
| **Finalized** | Concept promoted to final folders |

---

## Concept Workflow Phases

| Phase | Status | Output |
|-------|--------|--------|
| **Gathering** | Collecting inputs | 01-INPUTS/INDEX.md |
| **Extracting** | Processing inputs | 02-EXTRACTIONS.md |
| **Conceptualizing** | Building concept | 03-CONCEPT.md |
| **Planning** | Creating work plan | 04-WORKPLAN.md |
| **Roadmapping** | Dependencies & timeline | 05-ROADMAP.md |
| **Finalizing** | Promoting outputs | concepts/, workplans/ |

---

## Folder Naming

| Pattern | Example | Meaning |
|---------|---------|---------|
| `NNN-TYPE-name` | `001-feat-auth` | Work item folder |
| `vN` | `v1`, `v2` | Version number |
| `90-OUTPUTS` | Work item subfolder | Deliverables |

---

## Commands Quick Reference

| Command | Purpose |
|---------|---------|
| `>>start` | Begin new work |
| `>>continue` | Resume existing work |
| `>>wrap` | End session with handoff |
| `>>pause` | Pause with full context |
| `>>status` | Check progress (read-only) |
| `>>test` | Create test checklist |
| `>>bug` | Report and investigate bug |
| `>>archive` | Complete and archive work |
| `>>checkpoint` | Mid-session knowledge capture |
| `>>init-knowledge` | Setup knowledge base |
| `>>scan-repo` | Map repository structure |

**Concept-specific**:
| Command | Purpose |
|---------|---------|
| `>>add-input` | Add input source |
| `>>extract` | Process inputs |
| `>>conceptualize` | Build concept |
| `>>plan` | Create work plan |
| `>>roadmap` | Generate roadmap |
| `>>refine` | Re-enter workflow at phase |
| `>>finalize` | Promote to final folders |
| `>>new-version` | Create major revision |
