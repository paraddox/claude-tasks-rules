# Development Workflow Rules

This document contains the core development workflow rules for PRD creation, task generation, and task list management. Follow these instructions precisely to maintain consistency and quality.

## File Structure
- `/tasks/` - Contains all PRDs and task lists
- `/tasks/prd-*.md` - Product Requirements Documents
- `/tasks/tasks-*.md` - Generated task lists from PRDs

## Technology Stack Context
The user is a software architect who works with:
- **Languages**: C++, Python, C#, JavaScript
- **Frontend**: Angular, React
- **Development Tools**: Claude Code v1.0.17

---

# PRD (Product Requirements Document) Creation Workflow

## When to Use
When the user requests a new feature or provides a brief description that needs to be turned into a structured PRD.

## Process
1. **NEVER start implementing immediately**
2. **ALWAYS ask clarifying questions first**
3. Generate PRD only after gathering sufficient detail
4. Save as `prd-[feature-name].md` in `/tasks/` directory

## Required Clarifying Questions
Before writing any PRD, ask these questions (adapt based on the prompt):

### Core Understanding
- "What problem does this feature solve for the user?"
- "Who is the primary user of this feature?"
- "What is the main goal we want to achieve?"

### Functionality Details
- "Can you describe the key actions a user should be able to perform?"
- "Could you provide a few user stories? (e.g., As a [type of user], I want to [perform an action] so that [benefit])"
- "What kind of data does this feature need to display or manipulate?"

### Scope and Boundaries
- "Are there any specific things this feature should NOT do (non-goals)?"
- "How will we know when this feature is successfully implemented?"
- "Are there any potential edge cases or error conditions we should consider?"

### Technical Context
- "Are there any existing design mockups or UI guidelines to follow?"
- "Are there any known technical constraints or dependencies?"

## PRD Structure Template
Use this exact structure for all PRDs:

```markdown
# [Feature Name] - Product Requirements Document

## Introduction/Overview
[Brief description of the feature and problem it solves]

## Goals
- [Specific, measurable objective 1]
- [Specific, measurable objective 2]

## User Stories
- As a [user type], I want to [action] so that [benefit]
- As a [user type], I want to [action] so that [benefit]

## Functional Requirements
1. The system must [specific functionality]
2. The system must [specific functionality]
3. The system must [specific functionality]

## Non-Goals (Out of Scope)
- [What this feature will NOT include]
- [Scope limitation]

## Design Considerations (Optional)
[UI/UX requirements, mockups, component mentions]

## Technical Considerations (Optional)
[Technical constraints, dependencies, integration notes]

## Success Metrics
- [How success will be measured]
- [Specific metrics or KPIs]

## Open Questions
- [Remaining questions or clarifications needed]
```

## Target Audience
Write PRDs for **junior developers** - be explicit, unambiguous, and avoid jargon.

---

# Task Generation from PRD Workflow

## When to Use
When the user wants to generate a task list from an existing PRD file.

## Two-Phase Process

### Phase 1: Generate Parent Tasks
1. Read and analyze the specified PRD file
2. Create high-level tasks (typically ~5 main tasks)
3. Present tasks WITHOUT sub-tasks yet
4. Say: **"I have generated the high-level tasks based on the PRD. Ready to generate the sub-tasks? Respond with 'Go' to proceed."**
5. **WAIT for user confirmation**

### Phase 2: Generate Sub-Tasks
1. Only proceed after user says "Go"
2. Break down each parent task into smaller, actionable sub-tasks
3. Identify relevant files that will be created/modified
4. Generate final output with complete structure

## Output Format
Save as `tasks-[prd-file-name].md` in `/tasks/` directory:

```markdown
## Relevant Files

- `path/to/file1.ts` - Brief description of purpose
- `path/to/file1.test.ts` - Unit tests for file1.ts
- `path/to/another/file.tsx` - Brief description
- `path/to/another/file.test.tsx` - Unit tests for another/file.tsx

### Notes

- Unit tests should be placed alongside code files
- Use `npx jest [optional/path/to/test/file]` to run tests
- Running without path executes all tests found by Jest configuration

## Tasks

- [ ] 1.0 Parent Task Title
  - [ ] 1.1 [Sub-task description]
  - [ ] 1.2 [Sub-task description]
- [ ] 2.0 Parent Task Title
  - [ ] 2.1 [Sub-task description]
- [ ] 3.0 Parent Task Title
```

---

# Task List Management Protocol

## Critical Rules - Follow Exactly

### One Sub-Task at a Time
- **NEVER start the next sub-task until you ask for permission**
- After completing any sub-task, ask: "Sub-task completed. Ready for the next one? (y/n)"
- **WAIT for user to say "yes", "y", or equivalent before proceeding**

### Completion Protocol
When you finish a **sub-task**:
1. **Immediately mark it completed**: Change `[ ]` to `[x]`
2. **Check parent task**: If ALL subtasks under a parent are now `[x]`, mark the parent as `[x]` too
3. **Update the task file** with the changes
4. **Pause and ask for permission** to continue

### Example of Proper Completion
```markdown
- [x] 1.0 Setup Project Structure (completed because all subtasks done)
  - [x] 1.1 Initialize repository
  - [x] 1.2 Setup TypeScript configuration
  - [x] 1.3 Install dependencies
- [ ] 2.0 Implement Core Features
  - [x] 2.1 Create user authentication (just completed)
  - [ ] 2.2 Build user dashboard (next to work on)
```

### File Maintenance
1. **Update task list file after each sub-task completion**
2. **Maintain "Relevant Files" section** - add any new files created/modified
3. **Add newly discovered tasks** as they emerge during implementation
4. **Keep file descriptions current** with one-line purpose statements

### Before Starting Work
1. **Check which sub-task is next** in the task list
2. **Confirm it's the right task** to work on
3. **Start implementation** only after confirmation

### After Completing Work
1. **Mark the sub-task as complete** `[x]`
2. **Update relevant files section** if needed
3. **Save the updated task file**
4. **Ask permission** before starting next sub-task

## Task Discovery and Updates
- Add new tasks as they become apparent during implementation
- Break down tasks that prove more complex than expected
- Update descriptions if scope changes
- Maintain parent-child relationships properly

---

# Implementation Guidelines

## File Creation and Modification
- Always update the "Relevant Files" section when creating/modifying files
- Include corresponding test files for code files
- Use descriptive one-line descriptions for each file's purpose

## Progress Tracking
- Task lists are the single source of truth for project progress
- Check completed tasks to understand what's already done
- Use task completion to guide next steps

## Communication Protocol
- Always ask before moving to next sub-task
- Be explicit about what was completed
- Show updated task list after each completion
- Confirm understanding before starting complex tasks

## Quality Assurance
- Each sub-task should be specific and actionable
- Sub-tasks should logically build toward parent task completion
- Maintain consistency in task numbering and formatting
- Keep descriptions clear for junior developers

---

# Custom Commands for Claude Code

Use these patterns when working with the development workflow:

## PRD Commands
- `/create-prd <feature-description>` - Start PRD creation process with clarifying questions
- `/review-prd <filename>` - Review existing PRD for completeness

## Task Commands  
- `/generate-tasks <prd-filename>` - Generate task list from PRD (two-phase process)
- `/next-task` - Identify next sub-task to work on
- `/complete-task <task-number>` - Mark task complete and update files
- `/task-status` - Show current progress on all tasks

## File Commands
- `/update-relevant-files` - Refresh the relevant files section
- `/create-test <filename>` - Create corresponding test file

Remember: This workflow prioritizes careful, step-by-step progress with explicit user approval at each stage. Never rush ahead or skip the permission-asking steps.
