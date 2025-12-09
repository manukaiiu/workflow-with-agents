## CONCEPT WORKFLOW

How would an extension look like that handles generating two things in combination:

- A concept (that can be very complex) and needs several rounds of creation and enhancements and changes.
- A WorkPackage/Task structure including a roadmap (more sequence of work, optional timestampled milestones)

### Areas of work to include

- analysing a variety of raw input files (chatgpt-conversations.json, descriptions.md, pdf files, etc.)
- extracting and maintaining information from raw input files
- working concept (concepts can be very complex, structured into multiple sub-concepts with overall concept and touching non-programing scopes / areas and tasks) 
- based on concept a work plan with phases / epics, work packages, development and management (clarification, conceptualize, etc.) tasks and subtasks. the actual structure of the workplan can be open for whatever a project needs - or specifically adjusted for software development projects using jira and thusly being limited to Epics and Stories (Tasks as subtasks of stories optional)
- a roadmap showing necessary workflow sequences and potential parallel possibilities with optional actual timeframes added.
- refinement cycles that jump in at any of the above steps, leading to consequential changes in all following steps (analysis, extraction, conceptualizing, work package updating, roadmap changes)

All of this needs a well documented useful workflow, without redundancies, with concise clarity and similar steps of starting, continuing, wrapping like the other workflows for features, maintenance and bugfixing.

Please take some time reflecting on this requirement, finding potential blind spots and challenges when co-creating such concepts and work plans together with an ai agent and include mitigation strategies in the concept.





## CONFLICT OF AI-AGENT LIVING INSIDE DEV-PROJECT-N

Solved easily with less headache if i just argue for the gitignore line in each project.



## Feature Folder generation

Observation: The ai agent generated:

001-<feature-name-A>
001-<feature-name-B>

So auto increment is not working properly. This needs better workflow definition to avoid wrong numbering.



## Knowledge maintenance

Observation: ai-agent did some research within the repos code and planning for a new feature, triggered by the >>start command.
The research results where not added to the knowledge documentation. Ensure this in the workflow definitions.



## FEEDBACK BY AGENT: Useful Commands Documentation

**Human question**: "Could/should there be a specific documentation file (in knowledge?) and workflow to collect and maintain useful commands the agent would like to have a lookup table for?"

**Analysis**: There are two types of commands to consider:

### Project-Specific Commands
These should go in `knowledge/COMMANDS.md`:
```markdown
# Useful Commands

## Build & Development
npm run start           # Start dev server
npm run build          # Production build
npm run lint           # Run linting

## Package Management
# Regenerate lock file with Nexus registry
rm package-lock.json && npm install
sed -i 's/registry\.npmjs\.org/nexus.corp.chax.at\/repository\/npm/g' package-lock.json

## Database
npx prisma db seed     # Seed database
npx prisma generate    # Generate Prisma client
npx prisma migrate dev # Run migrations

## Debugging
git status             # Check uncommitted changes
npm audit              # Security check
```

### Generic Agent Commands
These can mostly be generated on-the-fly based on:
- Reading package.json scripts
- Common patterns (git, npm, etc.)
- Project knowledge

**Recommendation**: Create `knowledge/COMMANDS.md` for project-specific commands and gotcha-prone operations. Generic commands don't need documentation.



## FEEDBACK BY AGENT: Context Loss During Long Sessions

**Problem**: There was a development session spanning multiple context windows. When context was summarized and continued, the agent had no automatic trigger to re-read knowledge files.

**Impact**: The agent didn't proactively update knowledge until the human explicitly asked at the end.

**Suggestion**: Add to FOR-AGENTS.md:
```markdown
### After Context Continuation
When a session is continued from a summary:
1. Re-read `ai-agent/knowledge/SYSTEM-OVERVIEW.md`
2. Check if the summary mentions files that should be updated
3. Proactively ask: "Should I update knowledge with insights from this session?"
```

### Human addition

That sounds great. It would be great if the agent does this before compression happens, in order to avoid loosing valuable insight details. Can this be done at a certain context usage percentage, so we can be sure it fits before compressing?



## FEEDBACK BY AGENT: No "Incremental Knowledge Update" Trigger
**Problem**: The protocol says to update knowledge "when you discover valuable insights" but there's no explicit reminder or checkpoint.

**Suggestion**: Add periodic knowledge checkpoint prompts in `>>wrap`:
```markdown
**Knowledge Check**:
- Did you discover patterns worth documenting?
- Were there gotchas that future agents should know?
- Should any subsystem docs be created/updated?
```

### Human addition

It is hard to know when a ">>wrap" instruction is optimal. I would like an agent to help weave this process into the workflow(s)



## FEEDBACK BY AGENT: Missing "Non-Feature Work" Protocol
**Problem**: The long development session was a dependency update - not really a "feature" in the traditional sense. The feature template felt slightly awkward for maintenance/upgrade work.

**Suggestion**: Add a `>>maintenance` command or a separate template for:
- Dependency updates
- Security audits
- Refactoring work
- Build system changes

These have different structures than feature development (no requirements in the traditional sense, more focus on compatibility and testing).

### Human addition

Maybe we should change the "feature folder" naming convention to something like this: 001-<TYPE>-<NAME>
With these types:
- Feature
- Maintenance
- Bug
- Concept and Planning



## FEEDBACK BY AGENT: Summary Continuation Loses Tool Context
**Problem**: When context is summarized for continuation, the agent loses awareness of:
- Which tools have been used
- What the current working state is
- Whether there are pending file changes

**Suggestion**: Add to FOR-AGENTS.md a "Context Continuation Checklist":
```markdown
## When Continuing from Summary
1. Check git status for uncommitted changes
2. Re-read last progress log entry
3. Verify any mentioned "in progress" work
4. Ask user about current state if unclear
```

#### Human addition

That would be great! I would love that to be part of the workflow and documentation. Could/should there be a specific documentation file (in knowledge?) and workflow to collect and maintain useful commands? Or can you come up with them on the fly anyways? -> This connects to the feedback item "Useful Commands Documentation"



## Additional Files in Feature Folder

### Analysis

During a longer session, the agent created multiple analysis files in the feature folder. I think this should partially be redirected to the knowledge folders - but: This is mostly analysis required for the current feature with very specific contextual information. Should there be a new document to collect analysis? And how can it be woven into the workflow, to not become a detached third wheel, but stays interconnected with the process and other files.

### PR Message

Especially for longer and larger feature sessions it gets difficult to create and maintain a good short and concise PR message. It would be nice to add this to the predefined templates in the workflow.