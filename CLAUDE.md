## Agents

Use agents even if user did not ask you to do it explicitly
Agents folder is .claude/agents/ (in current project folder)

Agent Naming Convention:
- Role-based: [role]-[specialization].md (e.g., python-pro.md, react-specialist.md)
- Domain-based: [domain]-[function].md (e.g., database-optimizer.md, api-designer.md)
- All lowercase with hyphens
- Self-documenting names indicate primary expertise

IMPORTANT: Before starting any subtask you MUST select the best agent and apply it

When to Skip Agent Loading:
- Trivial tasks (< 2 minutes, single-step operations)
- Tasks already in progress with loaded agent
- Quick clarification questions from user
- Simple file reads or status checks
Always use agents for: code writing, analysis, design, debugging, testing, documentation
DO NOT use the Task tool to spawn subprocess agents - always use in-session agent loading instead.
Load ONLY ONE agent at a time - NEVER read multiple agent files in a single step
Agent instructions are TEMPORARY and apply only to the specific subtask at hand
Do NOT carry over agent-specific patterns, checklists, or conventions to unrelated subtasks

Agent Discovery Methods:
1. Check agent descriptions: Use Glob to list all agents: `*.md`
2. Search by domain: Use Grep to find agents by keyword in descriptions
3. Review Trigger Conditions: Each agent has "## Trigger Conditions" section listing when to load it
4. When uncertain: Prefer specialized agents over general ones (e.g., python-pro over fullstack-developer for Python tasks)

Agent Lifecycle:
- Agent context STARTS: When you read the agent file
- Agent context ACTIVE: During the specific subtask only
- Agent context ENDS: When subtask completes or you start reading a different agent
- Context isolation: Do NOT mix patterns from multiple agents in the same subtask

User request execution workflow MUST be like this:
1. Check available agents in agents folder
2. Parse the user request and list ALL implied subtasks
3. Map each subtask to the best agent
4. Report to user: "I identified these subtasks: [list] and will use these agents: [list]"

Agent Selection Priority (when multiple agents could apply):
1. Most specialized agent wins (e.g., postgres-pro over database-optimizer for PostgreSQL)
2. For overlapping domains, choose based on primary task focus:
   - Performance issues → performance-engineer
   - Security issues → security-auditor
   - Code quality → code-reviewer
3. For truly hybrid tasks, split into separate subtasks with different agents
4. Document your selection reasoning in the report to user

Subtask execution workflow MUST be like this:
1. Read the appropriate agent markdown file from agents folder using the Read tool (always fresh re-read)
   - Review "## Trigger Conditions" to confirm agent is appropriate
   - Follow "## Initial Assessment" steps immediately after loading
2. Apply those instructions to the CURRENT SUBTASK ONLY
3. COMPLETE the agent-guided work fully before proceeding
4. VERIFY work meets agent's quality standards and checklists
5. Save report for current subtask (you can use temporary folder if needed)
6. DISCARD the agent instructions - do not apply them to subsequent subtasks and return to default behavior
7. Proceed with next subtask using the same workflow
8. Once all subtasks are finished, compose all reports into one full report

Subtask Report Format:
Each subtask report should include:
1. Agent used: [agent-name]
2. Task description: [what was done]
3. Key findings/results: [bulleted list]
4. Quality verification: [checklist items verified]
5. Files modified: [list of changed files]
6. Next steps/recommendations: [if applicable]

Error Handling:
- If no suitable agent exists: Proceed with default behavior and document why no agent was selected
- If agent instructions conflict with task: Adapt agent guidance to task context, prioritize user's explicit requirements
- If agent work fails quality check: Re-attempt with same agent or try related agent
- If subtask scope changes mid-execution: Re-evaluate agent selection and reload if needed

Examples of subtasks which MUST use in-session agent instructions:

**Development & Code:**
- Python code changes → python-pro.md
- JavaScript/TypeScript code → javascript-pro.md or typescript-pro.md
- React development → react-specialist.md
- API design → api-designer.md or api-documenter.md
- Database work → database-optimizer.md or postgres-pro.md
- Debugging → debugger.md
- Code review → code-reviewer.md
- Refactoring → refactoring-specialist.md

**Analysis & Testing:**
- Log analysis → performance-engineer.md or data-analyst.md
- Performance analysis → performance-engineer.md
- QA checks → qa-expert.md
- Security audit → security-auditor.md or penetration-tester.md
- Accessibility testing → accessibility-tester.md

**Architecture & Design:**
- System design → cloud-architect.md or microservices-architect.md
- UI/UX design → ui-designer.md or ux-researcher.md
- Data modeling → data-engineer.md

**Infrastructure & Operations:**
- DevOps tasks → devops-engineer.md
- Kubernetes → kubernetes-specialist.md
- CI/CD → deployment-engineer.md
- Monitoring → sre-engineer.md

**Documentation & Communication:**
- Technical writing → technical-writer.md or documentation-engineer.md
- API documentation → api-documenter.md
