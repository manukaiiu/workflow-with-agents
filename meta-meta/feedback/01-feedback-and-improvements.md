# CURRENT FEEDBACK AND IMPROVEMENTS

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


## Feedback for Phase-3-concept

After reviewing the PHASE-3-concept.md i have these remarks. Open questions answering is located at the end of this list.

### Limitations

The document length limits are nice, if easily possible, to make it easier to digest. But if the actual concept needs more space, it is totally fine to exceed the limits.

### Commands

Commands look nice, but also: When the human talks to the agent without a specific command, let the agent do a pre-analysis to see if the human prompt matches the purpose of one of the commands and follow the pre-defined workflow automatically if the agent matches the command with confidence.

### Folders for concept work

Concept work is something more fundamental than a NNN-<type>-<name> feature/bug/maintenance task. Structurally it is similar to the knowledge folder.
I am not 100% certain if concedpt and plan (work-plan, tasks, roadmap) should be separate again, or mixed in with the concept.

Don't get me wrong. For creating the concept and workplan it seems appropriate to have then in a work/... folder. But the final resulting concept and work-plan should be on the top level of the folder structure i think.

Or, as i only read later in your Phase-3-concept.md, go ahead and merge the concept for storing conceptual information into the knowledge folder. Not sure if knowledge is then still the proper hypernym. Work-Plan is then not inside knowledge for sure.

### Versioning

This is totally missing so far. When working for a few days and sessions on a concept, a single version is fine. But sometimes a few weeks go by, new inputs accumulate, new meetings with project partners happen, and a lot changes with an "iteration". 

For one, this should probably result in a new work/... sub-folder.
And to keep such large changes better separated, the concept and workplan folders could be composed into versions, represented by their respective folders aswell. This keeps large version steps easier to separate, than the normal git history allows.

Later addition after reading the whole Phase-3-concept.md - please weave that into the knowledge folder concept (if that is the chosen path):

### Handling Open Questions during workflows

The agent(s) will definetly come back with Open Questions. For every spot in the workflows prepare a predefined section where the human can add their answers and reflections before pointing the agent to them and let them iterate on the new information and answers.

### Roadmap

Please include a mermaid version for quick visual examination of the roadmap. 
This could be an additional kind of "export" file that is generated on the fly, but not used as storing/maintaining information.

### Challenge 1: Input Format Diversity

If chatgpt conversations are in the input data, do not treat them as "just focus on conclusions and decisions". We are designing this system especially for one use-case where there is an immensely large (more than 10000 lines) conversation where every message contains essential information. We need to process and walk through such gigantic inputs with care and high attention to details.

### Challenge 2: Concept Scope Creep

Your mitigation suggestions are perfect. Except the hard limit on length. This needs to be more flexible.

### Challenge 3: Traceability loss

Your mitigation suggestions are great. One thing i have noticed with updating cross-references is, that this must be very explicit for agents to really do it whenever it is required. Please make sure it is properly documented in the created workflows.

### Challenge 4: Over-Engineering vs Under-Specification

Love your mitigations.

### Challenge 5: Context Window Limits

Remarks for mitigations: 
- Document max length is good, but it is hard to know when to enforce it, and when it would be destructive to the concept. This needs careful evaluation.
- `>>checkpoint` usage sounds great. But it is very hard for humans to know when this is required. Please add workflow steps for the agent at appropriate spots to let the agent analyse and decide if it would prefer to set a checkpoint and do it.

### Challenge 6: HUman-AI Alignment on Abstract Concepts

Love your mitigations.

### Challenge 7: Work Plan Format Flexibility

Mitigation sounds great. Please make sure the agent asks the user which format to use, before generating the wrong one.

### Open Questions for Human Input - Answers

1. **Input handling**: Should we support URL fetching directly, or require manual download? Yes, let's support URL fetching.

2. **PDF parsing**: Given AI limitations with PDFs, should we require human-provided summaries or attempt extraction? Let's attempt extraction with a human confirmation step.

3. **Work plan export**: Should we support direct export to Jira/GitHub APIs, or just generate markdown? Markdown is enough for the first trials.

4. **Timeline handling**: How detailed should time estimates be? Relative (waves) vs absolute (dates)? Relative is sufficient for the first trials.

5. **Concept complexity**: What's the maximum recommended number of sub-concepts before splitting into multiple concept efforts? Let's say 7, that fits nicely into the typical psychological context window of humans.

6. **Refinement triggers**: Should the agent proactively suggest refinement when detecting inconsistencies? Yes please.




=====================================================================

# OUTDATED (because already implemented) FEEDBACK


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