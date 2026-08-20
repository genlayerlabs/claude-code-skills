# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Repository Overview

This repository is a plugin marketplace (`genlayerlabs`) for [Claude Code](https://claude.ai/code) and [Codex](https://github.com/openai/codex). It provides installable plugins that guide AI assistants through complex operational procedures.

### Installation

```bash
# Claude Code
/plugin marketplace add genlayerlabs/skills
/plugin install genlayer-dev@genlayerlabs
/plugin install genlayernode@genlayerlabs

# Codex
codex plugin marketplace add genlayerlabs/skills
# Then enable plugins from Codex's plugin menu
```

## Marketplace Structure

```
.claude-plugin/
  marketplace.json              # Claude Code marketplace manifest
.agents/
  plugins/
    marketplace.json            # Codex marketplace manifest
plugins/
  <plugin-name>/
    .claude-plugin/
      plugin.json               # Claude Code plugin manifest
    .codex-plugin/
      plugin.json               # Codex plugin manifest
    .mcp.json                   # MCP server config (optional)
    skills/
      <skill-name>/
        SKILL.md                # Skill entry point with frontmatter
        skill.yaml              # Machine-readable procedure definition
        validations.yaml        # Automated checks (pre/post)
        sharp-edges.yaml        # Known edge cases and gotchas
        collaboration.yaml      # Dependencies and composition
        agents/
          openai.yaml           # Codex agent interface (optional)
```

## Skill Architecture

Each skill is defined by multiple YAML/Markdown files:

- **SKILL.md** - Human-readable documentation with full procedure details, step-by-step instructions, and usage examples
- **skill.yaml** - Machine-readable procedure definition including inputs, patterns, anti-patterns, config wizard structure, and the main procedure flow
- **validations.yaml** - Automated checks (prerequisites, post-installation verification) with commands, expected results, and error messages
- **sharp-edges.yaml** - Known edge cases and gotchas with detection commands, impact descriptions, and fixes. These must be **proactively checked** during execution, not just used for reactive diagnosis
- **collaboration.yaml** - Dependencies on external tools and skill composition sequences

## Key Concepts

### Skill Structure
Skills follow a decision-tree pattern with:
- **Decision points** - Questions that branch the procedure
- **Patterns** - Reusable command sequences for common operations
- **Anti-patterns** - Things to avoid with explanations of why they're bad
- **Defaults** - Sensible default values

### Sharp Edges Philosophy
Edge cases in `sharp-edges.yaml` must be checked **before** each major phase, not after failures occur. Each edge includes:
- `detect` - How to identify the issue
- `impact` - What goes wrong if not addressed
- `fix` - How to resolve it
- `severity` - critical/high/medium

### Validation Timing
- `on_stop` validations - Must pass before procedure proceeds
- `on_warn` validations - Warnings that don't block but should be addressed

## Working with Skills

When modifying skills:
1. Keep SKILL.md and skill.yaml in sync - they describe the same procedure
2. Add new edge cases to sharp-edges.yaml when discovering failure modes
3. Add validation commands to validations.yaml for automated checking
4. Update collaboration.yaml when adding new dependencies or composition sequences

When a skill is invoked:
1. Display process overview at start
2. Check prerequisites from validations.yaml
3. Follow procedure from skill.yaml, checking sharp-edges.yaml proactively at each phase
4. Use config_wizard structure for interactive configuration
5. Run post-installation validations

## Website

The file `index.html` is the public-facing website for this marketplace. It displays all **plugin skills** (from `plugins/`) organized into Build and Operate sections. It does NOT include internal development skills (from `.claude/skills/`).

When you add, remove, or modify a plugin skill's description, name, or content, you **must** update `index.html` to reflect the change. The skill data lives in the `skills` JavaScript object inside the `<script>` tag, organized by section (`build` and `operate`).

## Security Constraints

Skills that handle secrets must follow strict masking requirements:
- Never display full API keys, passwords, or tokens
- Never execute remote commands that would expose secrets in output
- Use placeholders in generated configs, instruct users to set values manually

## Review-Ready Bar

Every change to this repo is held to this bar. **Report work as "REVIEW-READY", never "done"** — "done" extends through the maintainer's review, CI, and merge, which is theirs to declare. Binary: no partial credit. If any item fails, say so plainly and name the blocker.

**Intent**

1. **It does what was asked.** Restate the requirement in the PR and trace each part to the evidence showing it was met. (Guards against a perfectly-tested implementation of the wrong thing.)
2. **Prefer one thing**, small enough to review in one sitting — a preference, NOT a gate; not always possible or convenient. What IS firm: a defect you find in your OWN work you fix immediately, without asking — and if you have a concern, ASK. A defect outside the diff gets recorded, not silently folded in and not dropped.

**Proof**

3. **Nothing goes to a PR untested.**
4. **Everything testable locally is tested locally, before pushing.** For this repo: `task claude:validate-skill -- --skill <name>` for every changed skill, `task claude:audit-skills`, `task claude:validate-skill-yaml`, `task docs:refresh-check`, and `shellcheck` on any changed shell script under `taskfiles/`. CI is not our test runner; anything reproducible locally must be caught locally, because CI costs real money.
5. **Validate the change end-to-end.** This repo has no dev-env/e2e runtime, so the equivalent is: run the affected skill's `validations.yaml` via `task claude:validate-skill`, and for any `index.html` change open it and confirm it renders and the affected skill card/modal is correct. The principle that must survive: everything testable locally is tested locally before pushing.

**The artifact**

6. **Read the entire diff yourself** — every line, including generated and vendored changes you caused (e.g. `docs/skills/REFERENCE.md` and the `<!-- SKILLS_TABLE_START/END -->` block regenerated by `task docs:refresh`).
7. **No known defects left in the diff** — including comments, help text and docs that assert something false. A WRONG COMMENT IS A DEFECT.
8. **Docs match actual behaviour, in the same PR.** For this repo: `README.md`, the generated `docs/skills/REFERENCE.md` and the CLAUDE.md Development-Skills table (run `task docs:refresh`), and `index.html` — a plugin skill's name/description/content change MUST update `index.html`'s `skills` object.
9. **Operationally ready.** Security surface considered (new external surface, secrets/keys, dependency and vendor-hash changes); new behaviour diagnosable from metrics/logs without reading source; config-schema compatibility and a way to back it out. State explicitly when a dimension does not apply.

**The boundary**

10. **REVIEW-READY = the PR is open and its checks are green** — without CI e2e, unless the maintainer requests it. The maintainer reviews and merges.
11. **This list is inspected and adapted.** Every escaped defect asks: which line would have caught it, and why did it not?

**Approval — needs the maintainer's go:** merges · `--admin` · external/irreversible actions outside the PR (Slack, releases, deploys).
**Forbidden, never even ask:** force-push to a shared branch (`main`) — always work through a PR. `main` is protected: 2 required reviews, code-owner approval, and signed commits (`required_signatures`).
**Not gated:** force-pushing your OWN PR branch (rebasing is routine), and fixing your own defects.

## Available Plugins

| Plugin | Skill | When to Use |
|--------|-------|-------------|
| `genlayernode` | `genlayernode` | Interactive wizard to set up a GenLayer validator node on Linux. |

## Development Skills

<!-- SKILLS_TABLE_START -->
| Skill | When to Use |
|-------|-------------|
| `commit` | Execute git commit with conventional commit message analysis |
| `create-skill` | Scaffold a new Claude Code skill using the multi-YAML patter |
| `docs-refresh` | Refresh documentation with deterministic generation from sou |
| `linear` | Create and manage Linear issues using templates for the GenL |
| `pr-create` | Creates GitHub pull requests with conventional commit-style  |
| `pr-merge` | Merge GitHub pull requests with strict CI validation. Never  |
| `validator-manage` | Manage GenLayer validators across testnets using the genlaye |
<!-- SKILLS_TABLE_END -->
