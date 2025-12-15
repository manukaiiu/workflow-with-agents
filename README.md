# Workflow with Agents

A structured meta-documentation system for human-AI collaboration on software projects.

## What is this?

A workflow system that helps AI agents and humans work together effectively. The system provides:

- **Multiple work types** - Features, maintenance, bugs, and concept work (analysis/planning)
- **Knowledge retention** - AI builds and maintains project knowledge across sessions
- **Clear workflows** - Simple `>>` commands that expand to full protocols
- **Zero context loss** - Resume work quickly with self-documenting work items
- **Hierarchical documentation** - Minimal always-loaded core, details loaded on-demand

## Quick Start

### 1. Copy to your project

In your project root:

    mkdir -p ai-agent
    cp -r meta ai-agent/

The agent will create work/, knowledge/, and other folders when needed.

### 2. Point the agent to the system

First time only - Tell the agent:

    Please read ai-agent/meta/CORE.md - this explains our workflow system.

The agent reads the core documentation (~200 lines) and loads protocol details on-demand.

### 3. Initialize knowledge

    Human: >>init-knowledge
    AI: [Asks questions, creates knowledge/SYSTEM-OVERVIEW.md]

    Human: >>scan-repo
    AI: [Scans your codebase]

### 4. Start work

    Human: >>start feat my-first-feature
    AI: [Creates work item folder, asks questions]

## Work Types

| Type | Command | Use For |
|------|---------|---------|
| Feature | >>start feat name | New functionality |
| Maintenance | >>start maint name | Updates, refactoring |
| Bug | >>start bug name | Fixing defects |
| Concept | >>start concept name | Analysis, planning, roadmaps |

## Core Commands

| Command | Purpose |
|---------|---------|
| >>start [type] name | Begin new work |
| >>continue | Resume existing work |
| >>wrap | End session (save progress) |
| >>pause | Interrupt with context saved |
| >>status | Quick status check |
| >>archive | Complete and archive work |

Concept work has additional phases: >>extract, >>conceptualize, >>plan, >>roadmap, >>finalize

## Documentation

| Audience | File |
|----------|------|
| Humans | meta/FOR-HUMANS.md |
| AI Agents | meta/CORE.md |
| Reference | meta/reference/ |

## Architecture

The system uses hierarchical loading to minimize context usage:

1. **CORE.md** (~200 lines) - Always loaded, navigation hub
2. **protocols/** - Loaded on-demand when commands are used
3. **reference/** - Consulted as needed for conventions

This replaced the previous monolithic FOR-AGENTS.md (1700+ lines).

## Folder Structure

    ai-agent/
    ├── meta/           # System docs (copied from this repo)
    │   ├── CORE.md
    │   ├── protocols/
    │   ├── reference/
    │   └── templates/
    ├── work/           # Active work items
    ├── knowledge/      # Project knowledge base
    ├── concepts/       # Finalized concepts
    └── workplans/      # Finalized work plans

## License

Free to use and modify for your projects.
