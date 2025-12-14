# AI Agents

These AI Agents are forked version of agents from Volt repository which can be found here: https://github.com/VoltAgent/awesome-claude-code-subagents. All agents are cleaned up from Volt-specific workflow leftovers.

In theory these agents are model-agnostic and can be used with any other LLM (but I am using them with Claude Code so this repository configured for such usage).

## Quick start (highly recommended)

1. **Copy files to your project**: Put `.claude/` folder (with `agents/` inside) into your Claude Code working directory

2. **Add instructions from CLAUDE.md to your model instructions file**: Copy the contents of `CLAUDE.md` into your project's instruction file (create one if it doesn't exist)

3. **Test it**: Ask Claude Code to perform any development task, for example: *"Review this Python code for security issues"* or *"Help me debug this performance bottleneck"*

Claude Code will automatically select and apply the most appropriate agent for each subtask.

## What it does and why you may need it (read this first)

Let me get right to the point and explain why I decided to fork these agents with custom instructions set. 

By default Claude Code uses agents like this: It creates Task() subprocess where agent do it's thing within it's own separate context (memory) and then prodives some kind of report which is used further. The agent's process is killed after that along with it's context and memories.

I find this workflow to be VERY inefficient, spending a lot of tokens and producing quite questionable results. 

Actually I think this is the main reason why agents works so bad and so many users stops using them. 
I used these agents quite a lot myself and can confirm this with my own experience.

Agents from this repository works differently: **They always use the same main context (shared memory) within current session and every agent is forcibly launched inside of the current session.**

Such approach provided numerous real-world benefits: Agents can re-use each own memories and research results, they spend MUCH less tokens, context, etc. At the same time the "pollution" problem which is usually used to justify separate processes is non-existent in my tests (I think that's because context gets compressed long before it becomes a problem).

Let me just spare the details and tell that **this way agents work MUCH better**, rather than running as separate processes. I highly recommend everyone to try this approch and check the results by yourself.

For best results I also recommend to combine these agents with web_search_agent I created which provides much better web search rather than the one included into Claude Code by default (check neigborhood repository for that).

---

## Features

- **115 Specialized Agents**: Covering development, DevOps, security, data science, ML/AI, and business domains
- **Automatic Agent Selection**: CLAUDE.md instructions guide Claude to pick the right agent for each subtask
- **In-Session Loading**: Agents load directly into the conversation context without spawning subprocesses
- **Structured Workflows**: Each agent includes step-by-step checklists and quality gates
- **Cross-Agent Collaboration**: Agents reference each other for complex multi-domain tasks
- **Zero Dependencies**: Pure markdown files - no tools or runtime required

## Agent Categories

### Development (40+ agents)
| Agent | Description |
|-------|-------------|
| `python-pro` | Modern Python 3.11+, async, type safety, data science |
| `typescript-pro` | Advanced TypeScript, full-stack development |
| `javascript-pro` | Modern ES2023+, Node.js ecosystem |
| `rust-engineer` | Systems programming, memory safety |
| `golang-pro` | High-performance microservices |
| `java-architect` | Enterprise Spring ecosystem |
| `csharp-developer` | .NET Core, ASP.NET |
| `cpp-pro` | Modern C++20/23, systems programming |
| `react-specialist` | React 18+, hooks, server components |
| `nextjs-developer` | Next.js 14+, App Router |
| `vue-expert` | Vue 3, Composition API |
| `angular-architect` | Angular 15+, enterprise patterns |
| `django-developer` | Django 4+, REST APIs |
| `rails-expert` | Rails 7+, Hotwire/Turbo |
| `laravel-specialist` | Laravel 10+, PHP 8.3+ |
| `flutter-expert` | Cross-platform mobile |
| `swift-expert` | iOS/macOS development |
| `kotlin-specialist` | Android, multiplatform |

### DevOps & Infrastructure (15+ agents)
| Agent | Description |
|-------|-------------|
| `devops-engineer` | CI/CD, containerization, cloud platforms |
| `kubernetes-specialist` | Container orchestration, cluster management |
| `terraform-engineer` | Infrastructure as code, multi-cloud |
| `cloud-architect` | AWS, Azure, GCP architecture |
| `sre-engineer` | Site reliability, SLOs, automation |
| `deployment-engineer` | Release automation, zero-downtime |
| `platform-engineer` | Internal developer platforms |

### Data & ML/AI (10+ agents)
| Agent | Description |
|-------|-------------|
| `data-scientist` | Statistical analysis, ML, visualization |
| `data-engineer` | ETL pipelines, data infrastructure |
| `ml-engineer` | Model deployment, serving |
| `mlops-engineer` | ML infrastructure, CI/CD for ML |
| `llm-architect` | LLM architecture, fine-tuning |
| `nlp-engineer` | Natural language processing |
| `data-analyst` | Business intelligence, visualization |

### Security & Quality (10+ agents)
| Agent | Description |
|-------|-------------|
| `security-engineer` | DevSecOps, vulnerability management |
| `penetration-tester` | Ethical hacking, security testing |
| `security-auditor` | Security assessments, compliance |
| `code-reviewer` | Code quality, best practices |
| `qa-expert` | Test strategy, quality processes |
| `test-automator` | Test frameworks, CI/CD integration |

### Architecture & Design (10+ agents)
| Agent | Description |
|-------|-------------|
| `architect-reviewer` | System design validation |
| `microservices-architect` | Distributed systems |
| `api-designer` | REST/GraphQL API design |
| `database-optimizer` | Query optimization, performance |
| `refactoring-specialist` | Safe code transformation |

### Business & Management (15+ agents)
| Agent | Description |
|-------|-------------|
| `product-manager` | Product strategy, roadmaps |
| `project-manager` | Planning, execution, delivery |
| `business-analyst` | Requirements, process improvement |
| `scrum-master` | Agile transformation |
| `technical-writer` | Documentation, API docs |

### Debugging & Operations (10+ agents)
| Agent | Description |
|-------|-------------|
| `debugger` | Issue diagnosis, root cause analysis |
| `performance-engineer` | Optimization, profiling |
| `incident-responder` | Rapid detection, resolution |
| `error-detective` | Error pattern analysis |

## Usage

### Automatic (recommended)

With CLAUDE.md instructions in place, simply ask Claude Code to perform any task:

```
"Review this code for security vulnerabilities"
→ Claude automatically loads code-reviewer.md and security-auditor.md

"Debug this performance issue"
→ Claude automatically loads debugger.md and performance-engineer.md

"Help me design a microservices architecture"
→ Claude automatically loads microservices-architect.md
```

### Manual

You can explicitly request a specific agent:

```
"Use the python-pro agent to review my code"
"Apply the kubernetes-specialist instructions for this deployment"
```

## Agent Structure

Each agent markdown file follows this structure:

```markdown
---
name: agent-name
description: Brief description of expertise
tools: Read, Write, Edit, Bash, Glob, Grep
---

[Role definition and expertise areas]

When invoked:
1. Context gathering steps
2. Analysis approach
3. Implementation workflow
4. Quality checkpoints

[Domain-specific checklists]
[Best practices and patterns]
[Communication protocols]
[Integration with other agents]
```

## Workflow

The CLAUDE.md instructions establish this workflow:

1. **Parse Request**: Identify all implied subtasks from user request
2. **Map Agents**: Select the best agent for each subtask
3. **Report Plan**: Inform user of subtasks and assigned agents
4. **Execute Sequentially**: For each subtask:
   - Load agent instructions (fresh read)
   - Apply instructions to current subtask only
   - Complete the work fully
   - Discard agent instructions
5. **Compose Report**: Combine all subtask reports into final output

## Complete Agent List

<details>
<summary>Click to expand full list of 115 agents</summary>

accessibility-tester, agent-organizer, ai-engineer, angular-architect, api-designer, api-documenter, architect-reviewer, backend-developer, blockchain-developer, build-engineer, business-analyst, chaos-engineer, cli-developer, cloud-architect, code-reviewer, competitive-analyst, compliance-auditor, content-marketer, context-manager, cpp-pro, csharp-developer, customer-success-manager, data-analyst, data-engineer, data-researcher, data-scientist, database-administrator, database-optimizer, debugger, dependency-manager, deployment-engineer, devops-engineer, devops-incident-responder, django-developer, documentation-engineer, dotnet-core-expert, dotnet-framework-4.8-expert, dx-optimizer, electron-pro, embedded-systems, error-coordinator, error-detective, fintech-engineer, flutter-expert, frontend-developer, fullstack-developer, game-developer, git-workflow-manager, golang-pro, graphql-architect, incident-responder, iot-engineer, java-architect, javascript-pro, knowledge-synthesizer, kotlin-specialist, kubernetes-specialist, laravel-specialist, legacy-modernizer, legal-advisor, llm-architect, machine-learning-engineer, market-researcher, mcp-developer, microservices-architect, ml-engineer, mlops-engineer, mobile-app-developer, mobile-developer, multi-agent-coordinator, network-engineer, nextjs-developer, nlp-engineer, payment-integration, penetration-tester, performance-engineer, performance-monitor, php-pro, platform-engineer, postgres-pro, product-manager, project-manager, prompt-engineer, python-pro, qa-expert, quant-analyst, rails-expert, react-specialist, refactoring-specialist, research-analyst, risk-manager, rust-engineer, sales-engineer, scrum-master, search-specialist, security-auditor, security-engineer, seo-specialist, spring-boot-engineer, sql-pro, sre-engineer, swift-expert, task-distributor, technical-writer, terraform-engineer, test-automator, tooling-engineer, trend-analyst, typescript-pro, ui-designer, ux-researcher, vue-expert, websocket-engineer, wordpress-master, workflow-orchestrator

</details>

## Customization

You can customize agents by:

1. **Modifying existing agents**: Edit markdown files to match your team's standards
2. **Adding new agents**: Create new `.md` files following the existing structure
3. **Adjusting CLAUDE.md**: Modify the workflow instructions to fit your needs

## License

MIT License
