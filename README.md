# AI Agents

109 specialized agents for Claude Code. Curated from 4 sources: affaan-m, lst97, wshobson, and supatest. Cleaned up and optimized for in-session loading.

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

## Features

- **109 Specialized Agents**: Development, DevOps, security, data science, ML/AI, business
- **Automatic Selection**: Claude picks the right agent for each subtask
- **In-Session Loading**: No subprocesses, shared context
- **Zero Dependencies**: Pure markdown files

## Agent Categories

| Category | Count | Examples |
|----------|-------|----------|
| Development | 30+ | python-pro, typescript-pro, react-pro, golang-pro |
| DevOps & Infra | 15+ | kubernetes-architect, terraform-pro, cloud-architect |
| Data & ML/AI | 10+ | data-scientist, ml-engineer, llm-architect |
| Security & QA | 15+ | security-reviewer, penetration-tester, code-reviewer |
| Architecture | 10+ | microservices-architect, api-designer, database-optimizer |
| Business & Design | 15+ | product-manager, ui-designer, ux-designer |
| Debugging | 10+ | debugger, performance-engineer, incident-responder |

<details>
<summary>Full list of 109 agents</summary>

agent-organizer, ai-engineer, api-designer, api-documenter, architect, backend-architect, backend-security-coder, bash-pro, build-error-resolver, build-engineer, c-pro, cli-developer, cloud-architect, code-reviewer, cpp-pro, csharp-pro, data-engineer, data-researcher, data-scientist, database-architect, database-optimizer, database-reviewer, debugger, deployment-engineer, design-system-architect, devops-engineer, devops-incident-responder, devops-troubleshooter, django-pro, docs-architect, doc-updater, documentation-pro, dotnet-core-pro, dotnet-framework-pro, dx-optimizer, e2e-runner, electron-pro, elixir-pro, event-sourcing-architect, fastapi-pro, flutter-pro, frontend-developer, frontend-security-coder, full-stack-developer, golang-pro, go-build-resolver, go-reviewer, graphql-architect, haskell-pro, hybrid-cloud-architect, incident-responder, ios-pro, java-pro, javascript-pro, julia-pro, kotlin-pro, kubernetes-architect, legacy-modernizer, llm-architect, mcp-developer, mermaid-pro, microservices-architect, mlops-engineer, mobile-developer, mobile-security-coder, monorepo-architect, network-engineer, nextjs-pro, observability-engineer, penetration-tester, performance-engineer, php-pro, planner, platform-engineer, posix-shell-pro, postgres-pro, product-manager, prompt-engineer, python-pro, python-reviewer, qa-pro, rails-pro, react-pro, refactor-cleaner, research-analyst, ruby-pro, rust-pro, scala-pro, security-reviewer, service-mesh-pro, sre-engineer, spring-boot-pro, swift-pro, tdd-guide, terraform-pro, test-automator, threat-modeling-pro, tutorial-engineer, typescript-pro, ui-designer, ux-designer, vector-database-engineer, vue-pro, websocket-engineer, wordpress-master

</details>

## License

MIT
