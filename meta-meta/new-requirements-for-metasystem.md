## Introduction and current state

Okay, as you can see from the *.md files in the meta directory, we are working on a meta documentation and cooperation workflow system, to enable humans and agents work on a programming project in tandem.

So far our system is nice and precise for a single feature development, within a project where the agent already has context about the project.

We have established these folder so far:

meta .. containing infos for humans and agents how to use the feature creation workflow
meta/templates .. template files for the agent to copy and fill for single sessions

The folders will copied into a folder-structure like this:

project-root
project-root/ai-agent/
project-root/ai-agent/meta
project-root/ai-agent/meta/templates

I want to further develop our system here.
Please keep up the beautiful precission you created so far. Avoid any duplicate information in multiple files. Keep it concise and easy to read up for humans.

This further development of this system contains multiple new features and workflows. So i would like you to create your own instruction, task planning and status documentation in the meta-meta folder, so you can nicely chunk the following information into steps, which you can ideally perform within your context and complexity limitations.

Please be extra careful to avoid redundancy and update all files that need it, if the new developments in here require it.


## New Features and some fixes

### Fix: Ensure agent compliance

In my recent test, i found that updating checkboxes for progress in the created files did not always work. Please add one remarks where they are most effective (probably in the FOR-AGENTS.md), to ensure agent compliance.

### Fix: Command system

The suggested command system does not work, because "/start" and other "/..." commands interfer with the claude command system. The commands cannot start with a slash. What would work for a agent-agnostic usage of this here metasystem? Please change the command prefix to something suitable and update the documentation in here.

### New Feature - Multiple features

The system works quite well for a single feature.
Lets update the documentation to support the following behavior:

Next to the meta folder i also want a "features" folder.
Resulting in a folder structure within a project like this:
project-root/ai-agent/features
I havae already created the empty folder.

Whenever the human starts a new feature, the agent should create a new subfolder: "<three-digit-count>_<concise-feature-name>"
Resulting in a folder structure within a projekt like these examples:
project-root/ai-agent/features/001_new-login-provider
project-root/ai-agent/features/002_password-reset-workflow

After creating the specific feature folder, all the feature development template files will be copied there and filled out. From that point on, the feature development documentation lives there.

To allow other workflows beside feature creation, i want you to move the current template files into a new subfolder like this:
/meta/templates/features/

Please update the according documentation in the FOR-AGENTS.md, FOR-HUMANS.md and README.md accordingly.

### New Feature - Knowledge collection and lookup

This is a totally new workflow. When copying this meta system to a new project, the agent needs to learn the content of the project. Some generic knowledge about the system first, more specific knowledge about sub-systems during the work within the project.

What i want is:
- a initial knowledge creation process (human and agent)
- a workflow for the agent, to add collected knowledge while co-developing features
- template files to cover both use-cases.

This means probably a new templates subfolder like this:
/meta/knowledge/
filled with templates according to your genius input.

Both new workflows need to be documented in the *.md files in the "meta" folder.

#### Initial Knowledge Creation

This could be just the standard "scan the repository" task for agents. But this does take up a whole lot of tokens, and might be possible to be done more effectively by partially scanning the repository and partially going through a QnA process with the human, where the agent asks what it needs to understand better.

I am not sure if all should be a QnA process or if ther also should be an initial system description template which the human can fill out, before starting the conversation with the agent.

So i see three knowledge creation workflows:
- human describes system and agent reads that, maybe stores its own version which is better for agentic understanding
- agent does a QnA session with the human and stores info accordingly
- agent scans through repository and stores found concepts and infos accordingly

I am not sure if this is a good set of workflows, or if there is something important missing, or agents prefer another set for learning a porject. Please add and modify this requirement as needed.

And also come up with the documentation file template content concept that is ideal for your purposes. Create as few or many files with the perfect content for agents to easily understand a project, document knowledge and update it.

Of course the feature-development workflow needs to point the agent to the knowledge directory and explain its architecture to allow an agent to easily retrieve the collected information as needed.

#### Incremental Knowledge Creation

While the initial knowledge creation probably mostly focuses on the big picture and some higher order concepts, working on single features digs deep into specific sub-systems. 

The knowledge the agent accumulates while working on a feature is helpful within this feature development session, but also later on if we revisit adjacent features.

I want the agent to have some small workflow that is integrated into any work - especially feature development - that ensures interesting concepts and important findings are documented within the knowledge folder.

So please come up with the according workflow and documentation templates.

Again the feature-development workflow needs to point the agent to the knowledge directory and explain its architecture to allow an agent to easily retrieve the collected information as needed.