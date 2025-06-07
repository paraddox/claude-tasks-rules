# Claude Tasks Rules

A comprehensive workflow system for Claude Code that provides structured Product Requirements Document (PRD) creation, task generation, and step-by-step task management with built-in approval gates.

**Compatible with all Claude Code configurations:**
- ✅ Claude Code via Anthropic API
- ✅ Claude Code with Claude Pro plans  
- ✅ Claude Code with Claude Max plans

## 🎯 What This Does

This rule set transforms Claude Code into a disciplined development workflow tool that:

- **Creates detailed PRDs** through guided questioning rather than assumptions
- **Generates comprehensive task lists** from PRDs using a two-phase approval process  
- **Enforces one-task-at-a-time execution** with explicit user permission between steps
- **Maintains project progress tracking** with automatic file updates and completion protocols
- **Ensures junior developer readability** with clear, unambiguous requirements

Originally converted from Cursor IDE rules to work seamlessly with Claude Code's conversational approach.

## 🚀 Quick Start

### Installation

1. **Download the file**: Save `claude-tasks-rules.md` to your project directory
2. **Import in your main CLAUDE.md**: Add this as the first line:

```markdown
@claude-tasks-rules.md

# Your Project Name
[Your existing Claude.md content continues here...]
```

3. **Create the tasks directory**:
```bash
mkdir tasks
```

### Basic Usage

1. **Create a PRD**: Ask Claude to create a PRD for any feature - it will ask clarifying questions first
2. **Generate tasks**: Request task generation from your PRD - uses two-phase approval
3. **Execute tasks**: Work through tasks one-by-one with automatic progress tracking

## 📋 Workflow Overview

### Phase 1: PRD Creation
```
User: "I want a user profile editing feature"
↓
Claude: Asks 6-8 clarifying questions about goals, users, scope, etc.
↓
User: Provides answers
↓
Claude: Generates detailed PRD saved as `/tasks/prd-user-profile-editing.md`
```

### Phase 2: Task Generation  
```
User: "Generate tasks from the user profile PRD"
↓
Claude: Creates high-level parent tasks only
Claude: "Ready to generate sub-tasks? Respond with 'Go' to proceed."
↓
User: "Go"
↓
Claude: Generates complete task breakdown saved as `/tasks/tasks-prd-user-profile-editing.md`
```

### Phase 3: Task Execution
```
Claude: Implements first sub-task
Claude: Marks task complete [x], updates files
Claude: "Sub-task completed. Ready for the next one? (y/n)"
↓
User: "y"
↓
Claude: Continues to next sub-task
[Repeat until all tasks complete]
```

## 📁 File Structure

The workflow creates and maintains this structure:

```
your-project/
├── CLAUDE.md                                    # Your main Claude file
├── claude-tasks-rules.md                       # This rules file
└── tasks/
    ├── prd-user-profile-editing.md             # Product Requirements
    ├── tasks-prd-user-profile-editing.md       # Generated task list
    ├── prd-payment-integration.md              # Another PRD
    └── tasks-prd-payment-integration.md        # Another task list
```

## 🛠 Features

### ✅ Disciplined PRD Creation
- **Never starts implementing without clarification**
- Asks targeted questions about goals, users, scope, and technical constraints
- Generates PRDs suitable for junior developers
- Maintains consistent structure across all PRDs

### ✅ Two-Phase Task Generation  
- **Phase 1**: Creates high-level parent tasks, waits for approval
- **Phase 2**: Breaks down into detailed sub-tasks after user confirmation
- Identifies all relevant files that will be created/modified
- Includes test file planning and execution notes

### ✅ Step-by-Step Execution
- **One sub-task at a time** - never rushes ahead
- **Explicit permission required** between each sub-task
- **Automatic progress tracking** with `[ ]` to `[x]` completion
- **Parent task completion** when all sub-tasks are done

### ✅ File Management
- Updates "Relevant Files" section as work progresses
- Maintains accurate one-line descriptions for each file
- Tracks both implementation and test files
- Preserves project organization standards

## 🎯 Example Usage

### Creating a New Feature PRD

**User Input:**
```
I need a user authentication system
```

**Claude Response:**
```
I'll help you create a PRD for a user authentication system. Before writing the PRD, I need to gather some details:

1. What problem does this authentication system solve for users?
2. Who are the primary users (end users, admins, developers)?
3. What key actions should users be able to perform (login, register, password reset)?
4. Are there any existing design mockups or UI guidelines to follow?
5. What are the technical constraints or security requirements?
6. How will we measure success of this feature?

[Continues with clarifying questions...]
```

### Generating Tasks from PRD

**User Input:**
```
Generate tasks from prd-user-authentication.md
```

**Claude Response:**
```
I have generated the high-level tasks based on the PRD:

- [ ] 1.0 Setup Authentication Infrastructure  
- [ ] 2.0 Implement User Registration
- [ ] 3.0 Implement Login System
- [ ] 4.0 Add Password Management
- [ ] 5.0 Create User Dashboard

Ready to generate the sub-tasks? Respond with 'Go' to proceed.
```

### Task Execution Flow

**Claude automatically:**
1. Implements the first sub-task
2. Marks it complete: `- [x] 1.1 Setup project dependencies`
3. Updates the task file
4. Asks: "Sub-task completed. Ready for the next one? (y/n)"
5. Waits for permission before continuing

## 🔧 Customization

### Technology Stack Context
The rules include context for software architects working with:
- **Languages**: C++, Python, C#, JavaScript  
- **Frontend**: Angular, React
- **Tools**: Claude Code v1.0.17

### Custom Commands
Built-in support for Claude Code slash commands:
- `/create-prd <feature-description>`
- `/generate-tasks <prd-filename>`
- `/next-task`
- `/complete-task <task-number>`
- `/task-status`

## 📚 Why This Approach

### Prevents Common Issues
- **Scope creep**: PRD creation forces clear boundaries  
- **Implementation rushing**: One-task-at-a-time prevents shortcuts
- **Missing requirements**: Clarifying questions catch edge cases
- **Progress confusion**: Explicit tracking shows exactly what's done

### Optimized for Teams
- **Junior developer friendly**: Clear, unambiguous instructions
- **Consistent output**: Same structure across all PRDs and tasks
- **Reviewable progress**: Task completion visible to whole team
- **Modular workflow**: Each phase can be reviewed independently

## 🤝 Contributing

This workflow system was converted from Cursor IDE rules to work with Claude Code. If you find improvements or have additional workflow patterns to add, contributions are welcome.

## 📄 License

MIT License - Feel free to adapt for your team's needs.

---

**Need help?** The workflow is designed to be self-guiding - just start with "I want to create a feature for..." and Claude will guide you through the process step by step.
