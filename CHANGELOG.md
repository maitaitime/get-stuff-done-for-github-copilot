# Changelog

All notable changes to GSD for Kilo Code will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [1.2.0] - 2025-02-03

### Added

- Codebase Indexing Tools integration (`list_code_definition_names`, `codebase_search`)
- Tool priority documentation for codebase exploration in README
- Tool strategy sections in 7 mode rules with usage guidance
- Semantic code search capability for debugging, verification, and integration checking

### Changed

- Updated 7 mode rules to include `list_code_definition_names` and `codebase_search`:
  - gsd-codebase-mapper, gsd-debugger, gsd-executor, gsd-integration-checker
  - gsd-verifier, gsd-plan-checker, gsd-roadmapper
- Enhanced gsd-codebase-mapper with detailed tool priority table and usage examples
- Enhanced gsd-debugger with codebase search guidance for finding related code
- Enhanced gsd-verifier with semantic search for goal verification
- Enhanced gsd-integration-checker with cross-phase connection discovery
- Enhanced gsd-executor with pattern-finding before implementation
- Enhanced gsd-plan-checker with feasibility verification against codebase

### Documentation

- Added 🔍 Codebase Indexing Tools section to README
- Documented tool priority: `list_code_definition_names` → `codebase_search` → `search_files` → `read_file`
- Added note about Codebase Indexing configuration requirements (Qdrant + embedding provider)

## [1.1.0] - 2025-02-03

### Added

- MCP tool priority system: Context7 → Web Search MCP → browser_action
- Recommended MCP Servers section in README with installation links
- Context7 MCP integration with `use_mcp_tool(context7, ...)` syntax
- Web Search MCP flexibility (Brave Search, Tavily, SearXNG, Perplexity)
- Tool equivalency table in README (Claude Code → Kilo Code mapping)

### Changed

- Converted all 11 mode rules from Claude Code to Kilo Code tool naming
- Converted all 22 workflows `allowed-tools` to Kilo Code syntax
- Updated discovery-phase skill with MCP priority hierarchy
- Updated research templates with Web Search terminology
- Replaced `mcp__context7__*` with `use_mcp_tool(context7, ...)` syntax
- Replaced `WebSearch`/`WebFetch` with `use_mcp_tool(web-search)` → `browser_action` pattern

### Attribution

- [Context7](https://github.com/upstash/context7) by Upstash for documentation MCP
- [Brave Search API](https://api.search.brave.com) as recommended Web Search MCP example

## [1.0.0] - 2025-02-02

### Added

- Initial Kilo Code adaptation of [glittercowboy/get-shit-done](https://github.com/glittercowboy/get-shit-done)
- 12 skills with proper YAML frontmatter for Kilo Code discovery
  - complete-milestone, diagnose-issues, discovery-phase, discuss-phase
  - execute-phase, execute-plan, list-phase-assumptions, map-codebase
  - resume-project, transition, verify-phase, verify-work
- 11 custom modes via `.kilocodemodes` for specialized agent behaviors
  - gsd-codebase-mapper, gsd-debugger, gsd-executor, gsd-integration-checker
  - gsd-phase-researcher, gsd-plan-checker, gsd-planner, gsd-project-researcher
  - gsd-research-synthesizer, gsd-roadmapper, gsd-verifier
- Mode-specific rules in `.kilocode/rules-{mode-slug}/` directories
- Workflow definitions in `.kilocode/workflows/`
- Project templates in `.gsd/templates/`

### Changed

- Restructured from Claude Code format to Kilo Code format
- Renamed `commands/` to `.kilocode/skills/`
- Renamed `agents/` to `.kilocode/rules-{mode-slug}/`
- Renamed `workflows/` to `.kilocode/workflows/`
- Renamed `templates/` to `.gsd/templates/`
- Removed npm installer and hooks (not needed for Kilo Code)

### Attribution

This project is a Kilo Code adaptation of the original [Get Shit Done](https://github.com/glittercowboy/get-shit-done) system created by [@glittercowboy](https://github.com/glittercowboy). All credit for the core GSD methodology, workflows, and agent designs belongs to the original author.
