# Changelog

All notable changes to GSD for GitHub Copilot will be documented in this file.

Format follows [Keep a Changelog](https://keepachangelog.com/en/1.1.0/).

## [Unreleased]

## [1.0.0] - 2025-02-04

### Added

- Initial GitHub Copilot port of [get-stuff-done-for-kilocode](https://github.com/punal100/get-stuff-done-for-kilocode) by [punal100](https://github.com/punal100)
- 27 Prompt Files with Copilot-compatible YAML frontmatter (`.github/prompts/*.prompt.md`)
  - Discovery, planning, execution, verification, and utility prompts
- 11 Custom Agents for specialized GSD behaviors (`.github/agents/*.agent.md`)
  - gsd-codebase-mapper, gsd-debugger, gsd-executor, gsd-integration-checker
  - gsd-phase-researcher, gsd-plan-checker, gsd-planner, gsd-project-researcher
  - gsd-research-synthesizer, gsd-roadmapper, gsd-verifier
- 12 Agent Skills with detailed instruction sets (`.github/skills/*/SKILL.md`)
  - complete-milestone, diagnose-issues, discovery-phase, discuss-phase
  - execute-phase, execute-plan, list-phase-assumptions, map-codebase
  - resume-project, transition, verify-phase, verify-work
- 9 Instructions for workflow guidelines (`.github/instructions/*.instructions.md`)
  - checkpoints, continuation-format, git-integration, model-profiles
  - planning-config, questioning, tdd, ui-brand, verification-patterns
- 18 Project templates in `.gsd/templates/` for context engineering documents
- Full 3-way tool mapping documentation (Claude Code → Kilo Code → GitHub Copilot)

### Changed

- Restructured from Kilo Code format to GitHub Copilot format
- Renamed `.kilocode/skills/` to `.github/skills/`
- Renamed `.kilocode/rules-{mode-slug}/` to `.github/agents/{agent}.agent.md`
- Renamed `.kilocode/workflows/` to `.github/prompts/`
- Renamed `.kilocode/rules/` to `.github/instructions/`
- Converted all tool references from Kilo Code to GitHub Copilot naming:
  - `read_file` → `readFile`
  - `write_to_file` → `editFiles`, `createFile`
  - `apply_diff` → `editFiles`
  - `execute_command` → `runInTerminal`
  - `search_files` → `textSearch`
  - `list_files` → `listDirectory`, `fileSearch`
  - `new_task` → `runSubagent`
  - `codebase_search` → `codebase`, `usages`
- Updated all 47 `.github/**/*.md` files with Copilot tool names and relative paths
- Updated all 18 `.gsd/templates/*.md` files with Copilot references
- Rewrote `update.prompt.md` from npm/npx workflow to git pull workflow
- Removed Kilo Code-specific files (`.kilocodemodes`, `.kilocode/` directory)

### Documentation

- Rewrote README.md with full attribution chain (Claude Code → Kilo Code → Copilot)
- Added 3-way structure comparison table (Claude Code | Kilo Code | GitHub Copilot)
- Added 4-column tool mapping table with all three platforms
- Added tool groups comparison by platform
- Added codebase exploration tools documentation
- Added MCP server support section

### Attribution

This project is a GitHub Copilot port of [GSD for Kilo Code](https://github.com/punal100/get-stuff-done-for-kilocode) by [@punal100](https://github.com/punal100), which itself is an adaptation of [Get Shit Done](https://github.com/glittercowboy/get-shit-done) by [@glittercowboy](https://github.com/glittercowboy). All credit for the core GSD methodology, workflows, and agent designs belongs to the original authors.
