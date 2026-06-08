# GenLayer Skills

A plugin marketplace providing skills for GenLayer development and operations. Works with [Claude Code](https://claude.ai/code) and [Codex](https://github.com/openai/codex).

## Installation

### Claude Code

```bash
# Add the marketplace
/plugin marketplace add genlayerlabs/skills

# Install a plugin
/plugin install genlayer-dev@genlayerlabs
/plugin install genlayernode@genlayerlabs
```

### Codex

```bash
codex plugin marketplace add genlayerlabs/skills
```

After adding the marketplace, enable individual plugins from Codex's plugin menu.

## Available Plugins

| Plugin | Description |
|--------|-------------|
| `genlayer-dev` | Development skills for intelligent contracts and apps — pinned GenVM runner versions, linting, tests, CLI workflows, and design-system guidance. |
| `genlayernode` | Interactive wizard to set up a GenLayer validator node on Linux. |

## Usage

After installing a plugin, invoke its skills:

### genlayer-dev

| Skill | Description |
|-------|-------------|
| `write-contract` | Write production-quality GenLayer intelligent contracts, including pinned runner headers, architecture fit, consensus boundaries, equivalence principles, storage rules, and LLM resilience |
| `genlayer-cli` | Deploy, interact with, and debug intelligent contracts using the GenLayer CLI |
| `genvm-lint` | Validate contracts with the GenVM linter |
| `direct-tests` | Write and run fast in-memory direct mode tests |
| `integration-tests` | Write and run integration tests against GenLayer environments |
| `genlayer-design` | Apply the GenLayer Design System to frontends, dashboards, demo apps, and screenshots |

### genlayernode

| Command | Description |
|---------|-------------|
| `/genlayernode install` | Install a new GenLayer validator node |
| `/genlayernode update` | Update an existing validator node to the latest version |
| `/genlayernode configure grafana` | Configure Grafana monitoring for your node |
