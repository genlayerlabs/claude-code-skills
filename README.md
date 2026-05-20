# GenLayer Skills

A [Claude Code](https://claude.ai/code) plugin marketplace providing skills for GenLayer development and operations.

## Installation

```bash
# Add the marketplace
/plugin marketplace add genlayerlabs/skills

# Install a plugin
/plugin install genlayer-dev@genlayerlabs
/plugin install genlayernode@genlayerlabs
```

## Available Plugins

| Plugin | Description |
|--------|-------------|
| `genlayer-dev` | Development skills for intelligent contracts — pinned GenVM runner versions, linting, direct mode tests, and integration tests. |
| `genlayernode` | Interactive wizard to set up a GenLayer validator node on Linux. |

## Usage

After installing a plugin, invoke its skills:

### genlayer-dev

| Skill | Description |
|-------|-------------|
| `write-contract` | Write contracts with pinned runner headers and production patterns |
| `genvm-lint` | Validate contracts with the GenVM linter |
| `direct-tests` | Write and run fast in-memory direct mode tests |
| `integration-tests` | Write and run integration tests against GenLayer environments |

### genlayernode

| Command | Description |
|---------|-------------|
| `/genlayernode install` | Install a new GenLayer validator node |
| `/genlayernode update` | Update an existing validator node to the latest version |
| `/genlayernode configure grafana` | Configure Grafana monitoring for your node |
