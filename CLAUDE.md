## Agents

Agents folder: `.claude/agents/`. Use agents for all non-trivial subtasks — code writing, analysis, design, debugging, testing, documentation.

**Rules:**
- Before any subtask: select the best agent and read its `.md` file (always fresh re-read)
- Load ONE agent at a time
- DO NOT use the Task tool for agents — use in-session agent loading instead
- Agent instructions are TEMPORARY — apply to current subtask only, discard after

**Discovery:** Consult `.claude/agents/INDEX.md` for the full agent directory (108 agents grouped by domain). Grep by keyword for specific needs. Prefer specialized over general agents.

### Request Workflow

1. **Plan:** For multi-step tasks, outline the plan before starting
2. **Decompose:** List subtasks, map each to best agent, report to user

**Agent selection:** Most specialized wins (e.g., postgres-pro over database-optimizer). Split hybrid tasks into subtasks with different agents.

### Subtask Workflow

1. Read agent `.md` → apply to current subtask → complete fully → verify quality
2. Discard agent instructions → next subtask
4. After all subtasks: compose into one report
