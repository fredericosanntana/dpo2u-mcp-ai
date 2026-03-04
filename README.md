# DPO2U MCP AI

**Model Context Protocol server** for LGPD compliance AI agents — provides standardized tools for querying on-chain compliance status, generating privacy documentation, and registering documents on IPFS.

## Overview

This repository contains the MCP server configuration, AI agent skills, and integration documentation for the DPO2U compliance protocol. It enables any AI agent (Claude, ChatGPT, or custom frameworks) to interact with the Midnight blockchain and DPO2U infrastructure via standardized tool calls.

## Skills

### Technical Skills

| Skill | Description | Based On |
|-------|-------------|----------|
| `code-explorer` | Codebase exploration and analysis | Claude Code Explore agent |
| `task-planner` | Complex implementation planning | Claude Code Plan agent |
| `shell-executor` | Safe command execution | Claude Code Bash tool |
| `web-researcher` | Web information retrieval | Claude Code WebSearch/WebFetch |
| `task-manager` | Task list management | Claude Code task tracking |
| `github-assistant` | GitHub operations via `gh` CLI | Claude Code GitHub integration |
| `code-reviewer` | Code review and analysis | Claude Code review capabilities |

### Cognitive Skills

| Skill | Description | Methodologies |
|-------|-------------|---------------|
| `brainstorming` | Creative idea generation | SCAMPER, Six Hats, Mind Map, HMW |
| `decision-maker` | Structured decision support | RICE, Decision Matrix, Pre-mortem, 10/10/10 |
| `problem-solver` | Root cause analysis | 5 Whys, RCA, PDCA, Fishbone |
| `project-kickoff` | Project initialization | Templates, RACI, ADRs |

## Repository Structure

```
dpo2u-mcp-ai/
├── skills/                    # Ready-to-use agent skills
│   ├── code-explorer/
│   ├── task-planner/
│   ├── shell-executor/
│   ├── web-researcher/
│   ├── task-manager/
│   ├── github-assistant/
│   ├── code-reviewer/
│   ├── brainstorming/
│   ├── decision-maker/
│   ├── problem-solver/
│   └── project-kickoff/
├── config/                    # Configuration examples
└── ESTUDO-INTEGRACAO-*.md     # Integration study
```

## Installation

```bash
# Copy all skills
cp -r skills/* ~/clawd/skills/

# Or copy a specific skill
cp -r skills/code-explorer ~/clawd/skills/
```

## Usage

Skills are invoked automatically based on context or manually:

```
Explore this project and give me an architecture overview
```

```
Plan the implementation of an authentication system
```

```
Run git status and show the repository state
```

## Configuration

Recommended model for best performance:

```json
{
  "agent": {
    "model": "anthropic/claude-opus-4-5"
  }
}
```

## Documentation

- [Integration Study](./ESTUDO-INTEGRACAO-CLAWDBOT-CLAUDE-CODE.md)
- [Claude Code Docs](https://docs.anthropic.com/claude-code)

## License

MIT
