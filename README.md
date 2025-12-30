# AI Agents

115 specialized agents for Claude Code. Forked from [VoltAgent](https://github.com/VoltAgent/awesome-claude-code-subagents), cleaned up and optimized for in-session loading.

## Quick Start

1. **Copy files**: Put `.claude/` folder into your Claude Code working directory
2. **Add instructions**: Copy `CLAUDE.md` contents into your project's instruction file
3. **Done**: Claude automatically selects the right agent for each task

## Why This Fork?

Default Claude Code spawns agents as separate subprocesses with isolated memory. This wastes tokens and produces poor results.

**This fork loads agents directly into the main session context.** Benefits:
- Agents share memory and research results
- Much lower token usage
- Significantly better output quality

Combine with [web_search_agent](https://github.com/anthropics/web_search_agent) for even better research capabilities.

## Features

- **115 Specialized Agents**: Development, DevOps, security, data science, ML/AI, business
- **Automatic Selection**: Claude picks the right agent for each subtask
- **In-Session Loading**: No subprocesses, shared context
- **Zero Dependencies**: Pure markdown files

## Agent Categories

| Category | Count | Examples |
|----------|-------|----------|
| Development | 40+ | python-pro, typescript-pro, react-specialist, rust-engineer |
| DevOps & Infra | 15+ | kubernetes-specialist, terraform-engineer, cloud-architect |
| Data & ML/AI | 10+ | data-scientist, ml-engineer, llm-architect |
| Security & QA | 10+ | security-engineer, penetration-tester, code-reviewer |
| Architecture | 10+ | microservices-architect, api-designer, database-optimizer |
| Business | 15+ | product-manager, technical-writer, scrum-master |
| Debugging | 10+ | debugger, performance-engineer, incident-responder |

<details>
<summary>Full list of 115 agents</summary>

accessibility-tester, agent-organizer, ai-engineer, angular-architect, api-designer, api-documenter, architect-reviewer, backend-developer, blockchain-developer, build-engineer, business-analyst, chaos-engineer, cli-developer, cloud-architect, code-reviewer, competitive-analyst, compliance-auditor, content-marketer, context-manager, cpp-pro, csharp-developer, customer-success-manager, data-analyst, data-engineer, data-researcher, data-scientist, database-administrator, database-optimizer, debugger, dependency-manager, deployment-engineer, devops-engineer, devops-incident-responder, django-developer, documentation-engineer, dotnet-core-expert, dotnet-framework-4.8-expert, dx-optimizer, electron-pro, embedded-systems, error-coordinator, error-detective, fintech-engineer, flutter-expert, frontend-developer, fullstack-developer, game-developer, git-workflow-manager, golang-pro, graphql-architect, incident-responder, iot-engineer, java-architect, javascript-pro, knowledge-synthesizer, kotlin-specialist, kubernetes-specialist, laravel-specialist, legacy-modernizer, legal-advisor, llm-architect, machine-learning-engineer, market-researcher, mcp-developer, microservices-architect, ml-engineer, mlops-engineer, mobile-app-developer, mobile-developer, multi-agent-coordinator, network-engineer, nextjs-developer, nlp-engineer, payment-integration, penetration-tester, performance-engineer, performance-monitor, php-pro, platform-engineer, postgres-pro, product-manager, project-manager, prompt-engineer, python-pro, qa-expert, quant-analyst, rails-expert, react-specialist, refactoring-specialist, research-analyst, risk-manager, rust-engineer, sales-engineer, scrum-master, search-specialist, security-auditor, security-engineer, seo-specialist, spring-boot-engineer, sql-pro, sre-engineer, swift-expert, task-distributor, technical-writer, terraform-engineer, test-automator, tooling-engineer, trend-analyst, typescript-pro, ui-designer, ux-researcher, vue-expert, websocket-engineer, wordpress-master, workflow-orchestrator

</details>

## License

MIT
