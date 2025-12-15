# Feedback: Domain-Specific Abbreviations Need Documentation

**ID**: FB-002
**Date**: 2025-12-09
**Source Project**: AID-CC Concept Work
**Category**: Documentation / Domain Knowledge
**Priority**: Medium
**Related**: FB-001

---

## Observation

In `03-CONCEPT-WP3.md`, the abbreviation "HCP" was used without definition. The human collaborator asked "what does HCP mean?"

**HCP** = Healthcare Professional

This is a domain-standard abbreviation in healthcare IT, but not universally known.

## Problem

1. **Domain knowledge assumed**: Agents may use industry-standard abbreviations without realizing they're not universally understood
2. **No first-use expansion**: Best practice is to expand abbreviations on first use, e.g., "Healthcare Professional (HCP)"
3. **Accumulated jargon**: Domain projects accumulate terminology that becomes a barrier to understanding

## Examples Found in AID-CC

| Abbreviation | Meaning | Domain |
|--------------|---------|--------|
| HCP | Healthcare Professional | Healthcare |
| EHR | Electronic Health Record | Healthcare |
| ELGA | Elektronische Gesundheitsakte (Austrian EHR) | Healthcare/AT |
| KG | Knowledge Graph | AI/ML |
| LLM | Large Language Model | AI/ML |
| RAG | Retrieval Augmented Generation | AI/ML |
| WCAG | Web Content Accessibility Guidelines | Web/A11y |
| HLEG | High-Level Expert Group | EU/Policy |
| MDR | Medical Device Regulation | EU/Regulatory |
| FHIR | Fast Healthcare Interoperability Resources | Healthcare/Standards |
| HL7 | Health Level 7 | Healthcare/Standards |

## Suggested Solution

### For Concept Documents

1. **First-use expansion rule**: Always expand abbreviations on first use in each document
2. **Document-level glossary**: Add a glossary section to concept documents with domain terms

### For Workflow System

Extend the glossary concept from FB-001 to include:
- **Workflow conventions** (T, R, C, etc.)
- **Domain terminology** (project-specific terms like HCP, ELGA)
- **Technical acronyms** (LLM, RAG, FHIR)

Structure could be:
```
ai-agent/meta/GLOSSARY.md
├── Workflow Conventions (T, R, C, Q, etc.)
├── Status Indicators ([x], [~], H/M/L)
└── [Project-specific sections added as needed]

ai-agent/work/[project]/GLOSSARY.md  (optional, project-specific)
├── Domain Terms (HCP, EHR, etc.)
└── Technical Terms (specific to this project)
```

## Recommendation

1. **Immediate**: Agents should expand abbreviations on first use
2. **Workflow enhancement**: Support project-level glossaries that accumulate domain knowledge
3. **Agent instruction**: Add guidance to FOR-AGENTS.md about abbreviation handling

---

## Meta

**Feedback Type**: Process Improvement + Agent Guidance
**Affects**: All concept templates, FOR-AGENTS.md
**Pattern**: "Expand on first use, collect in glossary"
