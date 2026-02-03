<div align="center">

# GSD for Kilo Code

**A Kilo Code port of the incredible [Get Shit Done](https://github.com/glittercowboy/get-shit-done) system by [glittercowboy](https://github.com/glittercowboy).**

This project adapts GSD's powerful context engineering and spec-driven development workflow to work natively with [Kilo Code](https://kilo.ai) using Skills and Custom Modes.

[![License](https://img.shields.io/badge/license-MIT-blue?style=for-the-badge)](LICENSE)

</div>

---

## 🙏 Credits & Attribution

> **This is a port, not an original work.**

All credit for the GSD system, methodology, and workflow design goes to:

### **[Get Shit Done](https://github.com/glittercowboy/get-shit-done)** by **[glittercowboy (TÂCHES)](https://github.com/glittercowboy)**

The original GSD is a brilliant meta-prompting and context engineering system for Claude Code. Everything good about this port comes from that project:

- The phase-based workflow (discuss → plan → execute → verify)
- Context engineering architecture (PROJECT.md, STATE.md, ROADMAP.md, etc.)
- Multi-agent orchestration patterns
- Goal-backward verification methodology
- Atomic commit strategies

**If you're using Claude Code, use the original:** https://github.com/glittercowboy/get-shit-done

**Join the GSD community:** [Discord](https://discord.gg/5JJgD5svVS)

---

## What This Port Does

This repository adapts GSD for **Kilo Code** by converting the system to use:

| Original (Claude Code)             | This Port (Kilo Code)              |
| ---------------------------------- | ---------------------------------- |
| Slash commands (`/new-project.md`) | Workflows (`.kilocode/workflows/`) |
| Agent prompts in `agents/`         | Custom Modes (`.kilocodemodes`)    |
| Claude Code specific paths         | Kilo Code conventions              |

### Tool Name Equivalency

Claude Code and Kilo Code use different tool naming conventions. This port uses Kilo Code tool names:

| Claude Code Tool         | Kilo Code Tool                    | Description                                                                |
| ------------------------ | --------------------------------- | -------------------------------------------------------------------------- |
| `Read`                   | `read_file`                       | Read file contents                                                         |
| `Write`                  | `write_to_file`                   | Create or overwrite files                                                  |
| `Edit`                   | `apply_diff`                      | Make surgical changes to files                                             |
| `Bash`                   | `execute_command`                 | Run terminal commands                                                      |
| `Grep`                   | `search_files`                    | Regex search across files                                                  |
| `Glob`                   | `list_files`                      | List directory contents                                                    |
| `Task`                   | `new_task`                        | Spawn subtasks/subagents                                                   |
| `AskUserQuestion`        | `ask_followup_question`           | Get user input                                                             |
| `TodoWrite`              | `update_todo_list`                | Track task progress                                                        |
| `WebSearch` / `WebFetch` | `use_mcp_tool` → `browser_action` | Documentation & web search (see [MCP Priority](#-recommended-mcp-servers)) |
| `SlashCommand`           | `switch_mode`                     | Change modes                                                               |
| `mcp__*`                 | `use_mcp_tool`                    | MCP server tools                                                           |

**Tool Groups (for Custom Modes):**

- `read` — `read_file`, `search_files`, `list_files`, `list_code_definition_names`, `codebase_search`
- `edit` — `apply_diff`, `write_to_file`, `delete_file`
- `browser` — `browser_action`
- `command` — `execute_command`
- `mcp` — `use_mcp_tool`, `access_mcp_resource`

For full tool documentation, see [Kilo Code Tools](https://kilo.ai/docs/automate/tools).

### 🔌 Recommended MCP Servers

GSD workflows that need documentation or web search use this **priority order**:

| Priority | Tool                                    | Purpose                          | When to Use                                                       |
| -------- | --------------------------------------- | -------------------------------- | ----------------------------------------------------------------- |
| 1️⃣       | **Context7 MCP**                        | Up-to-date library documentation | First choice for API docs, code examples, library usage           |
| 2️⃣       | **Web Search MCP** (e.g., Brave Search) | Real-time web search             | When Context7 doesn't have the library or need broader search     |
| 3️⃣       | `browser_action`                        | Full browser automation          | Fallback when MCPs unavailable or need to interact with web pages |

#### Context7 MCP

[Context7](https://github.com/upstash/context7) by **Upstash** provides up-to-date, version-specific documentation directly to your LLM. No more hallucinated APIs or outdated code examples.

**Available Tools:**

- `resolve-library-id` — Find Context7 library IDs
- `query-docs` — Get documentation for a specific library

**Installation:** See [Context7 Installation Guide](https://context7.com/docs/resources/all-clients)

**Free API Key:** [context7.com/dashboard](https://context7.com/dashboard)

#### Web Search MCP

For real-time web search, you can use **any** web search MCP server. Popular options include:

- **[Brave Search MCP](https://api.search.brave.com)** — Privacy-first search with independent index
- **Tavily** — AI-optimized search
- **SearXNG** — Self-hosted meta-search
- **Perplexity** — AI-powered search

**Brave Search Features:**

- `brave_web_search` — General web queries
- `brave_local_search` — Local business search
- `brave_news_search` — News articles

**Free API Key:** [api.search.brave.com/app/keys](https://api.search.brave.com/app/keys)

> **Note:** Users can install and configure any web search MCP that fits their needs. The workflows use `use_mcp_tool` which works with any compatible MCP server.

### Included

- **27 Workflows** — Discovery, planning, execution, verification workflows
- **11 Custom Modes** — Specialized agent modes (planner, executor, verifier, debugger, etc.)
- **Templates** — All GSD document templates adapted for Kilo Code

---

## 🚀 Getting Started

### PowerShell (Windows)

```powershell
# Open your project
cd your-project

# Clone the GSD template
git clone https://github.com/punal100/get-stuff-done-for-kilocode.git gsd-template

# Copy to your project
Copy-Item gsd-template\.kilocodemodes .\
Copy-Item -Recurse gsd-template\.kilocode .\
Copy-Item -Recurse gsd-template\.gsd .\

# Clean up
Remove-Item -Recurse -Force gsd-template
```

### Bash (Linux/Mac)

```bash
# Open your project
cd your-project

# Clone the GSD template
git clone https://github.com/punal100/get-stuff-done-for-kilocode.git gsd-template

# Copy to your project
cp gsd-template/.kilocodemodes ./
cp -r gsd-template/.kilocode ./
cp -r gsd-template/.gsd ./

# Clean up
rm -rf gsd-template
```

Then reload VS Code and use the `new-project` skill to get started.

---

## Installation

1. Clone or copy this repository into your project
2. Reload VS Code to pick up the skills and modes
3. The skills will appear in Kilo Code's skill selector

### Structure

```
.kilocode/
├── skills/
│   ├── complete-milestone/
│   ├── diagnose-issues/
│   ├── discovery-phase/
│   ├── discuss-phase/
│   ├── execute-phase/
│   ├── execute-plan/
│   ├── list-phase-assumptions/
│   ├── map-codebase/
│   ├── resume-project/
│   ├── transition/
│   ├── verify-phase/
│   └── verify-work/
├── rules/                    # Global rules for all modes
├── rules-gsd-executor/       # Mode-specific rules
├── rules-gsd-planner/
├── rules-gsd-verifier/
│   └── ...
└── workflows/                # Workflow definitions

.kilocodemodes                # 11 custom agent modes

.gsd/                         # Project planning data (created per-project)
├── PROJECT.md                # Project vision
├── REQUIREMENTS.md           # Scoped requirements
├── ROADMAP.md                # Phase structure
├── STATE.md                  # Current position, decisions, memory
├── config.json               # GSD settings
├── research/                 # Domain research outputs
│   ├── STACK.md
│   ├── FEATURES.md
│   ├── ARCHITECTURE.md
│   ├── PITFALLS.md
│   └── SUMMARY.md
├── codebase/                 # Codebase analysis (from map-codebase)
│   ├── STACK.md
│   ├── ARCHITECTURE.md
│   ├── STRUCTURE.md
│   ├── CONVENTIONS.md
│   ├── TESTING.md
│   ├── INTEGRATIONS.md
│   └── CONCERNS.md
├── phases/                   # Phase-specific files
│   ├── 01-CONTEXT.md
│   ├── 01-RESEARCH.md
│   ├── 01-PLAN.md
│   ├── 01-SUMMARY.md
│   ├── 01-VERIFICATION.md
│   └── ...
├── milestones/               # Archived milestones
├── debug/                    # Debug session files
├── quick/                    # Quick mode task files
└── todos/                    # Captured ideas for later
```

---

## How GSD Works

> All methodology credit goes to the [original GSD project](https://github.com/glittercowboy/get-shit-done).

### The Core Loop

1. **Initialize** — Define project, research domain, create roadmap
2. **Discuss** — Capture your implementation preferences
3. **Plan** — Research and create atomic task plans
4. **Execute** — Run plans with fresh context per task
5. **Verify** — Confirm goals were achieved, not just tasks completed

### Why It Works

- **Context engineering** — Right information at the right time
- **Fresh context per plan** — No degradation from accumulated tokens
- **Goal-backward verification** — Check outcomes, not just task completion
- **Atomic commits** — Every task gets its own traceable commit

For full documentation on the GSD methodology, see the [original project](https://github.com/glittercowboy/get-shit-done).

---

## Skills Reference

| Skill                    | Purpose                             |
| ------------------------ | ----------------------------------- |
| `complete-milestone`     | Archive milestone, tag release      |
| `diagnose-issues`        | Debug UAT gaps with parallel agents |
| `discovery-phase`        | Research before planning            |
| `discuss-phase`          | Capture implementation decisions    |
| `execute-phase`          | Run plans in parallel waves         |
| `execute-plan`           | Execute single plan with commits    |
| `list-phase-assumptions` | Surface assumptions before planning |
| `map-codebase`           | Analyze existing codebase           |
| `resume-project`         | Restore context when resuming       |
| `transition`             | Move to next phase                  |
| `verify-phase`           | Goal-backward verification          |
| `verify-work`            | User acceptance testing             |

---

## Custom Modes

| Mode                          | Purpose                        |
| ----------------------------- | ------------------------------ |
| 🗺️ `gsd-codebase-mapper`      | Analyze codebase structure     |
| 🐛 `gsd-debugger`             | Scientific debugging           |
| ⚡ `gsd-executor`             | Execute plans atomically       |
| 🔗 `gsd-integration-checker`  | Verify cross-phase integration |
| 🔬 `gsd-phase-researcher`     | Research phase implementation  |
| ✅ `gsd-plan-checker`         | Verify plans before execution  |
| 📋 `gsd-planner`              | Create executable plans        |
| 🌐 `gsd-project-researcher`   | Research domain ecosystem      |
| 📊 `gsd-research-synthesizer` | Synthesize research outputs    |
| 🛤️ `gsd-roadmapper`           | Create project roadmaps        |
| 🔍 `gsd-verifier`             | Verify goal achievement        |

---

## Contributing

This port aims to faithfully adapt GSD for Kilo Code. Contributions that improve the Kilo Code integration are welcome.

For improvements to the core GSD methodology, please contribute to the [original project](https://github.com/glittercowboy/get-shit-done).

---

## License

MIT License — Same as the original GSD project.

---

<div align="center">

**Original GSD by [glittercowboy](https://github.com/glittercowboy) — Kilo Code port**

⭐ **Star the original:** https://github.com/glittercowboy/get-shit-done

</div>
