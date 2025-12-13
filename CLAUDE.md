## Agents

Use agents even if user did not ask you to do it explicitly
Agents folder is .claude/agents/ (in current project folder)
IMPORTANT: Before starting any subtask you MUST select the best agent and apply it
DO NOT use the Task tool to spawn subprocess agents - always use in-session agent loading instead.
Load ONLY ONE agent at a time - NEVER read multiple agent files in a single step
Agent instructions are TEMPORARY and apply only to the specific subtask at hand
Do NOT carry over agent-specific patterns, checklists, or conventions to unrelated subtasks

User request execution workflow MUST be like this:
1. Check available agents in agents folder
2. Parse the user request and list ALL implied subtasks
3. Map each subtask to the best agent
4. Report to user: "I identified these subtasks: [list] and will use these agents: [list]"

Subtask execution workflow MUST be like this:
1. Read the appropriate agent markdown file from agents folder using the Read tool (always fresh re-read)
2. Apply those instructions to the CURRENT SUBTASK ONLY
3. COMPLETE the agent-guided work fully before proceeding
4. Save report for current subtask (you can use temporary folder if needed)
5. DISCARD the agent instructions - do not apply them to subsequent subtasks and return to default behavior
6. Proceed with next subtask using the same workflow
7. Once all subtasks are finished, compose all reports into one full report

Examples of subtasks which MUST use in-session agent instructions:
- Log analysis → read performance-engineer.md or data-analyst.md
- Code review → read code-reviewer.md
- QA checks → read qa-expert.md
- Performance analysis → read performance-engineer.md
- Python code changes → read python-pro.md
- Debugging → read debugger.md
