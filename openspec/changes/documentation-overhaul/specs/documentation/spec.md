## ADDED Requirements

### FR-001: Architecture Overview Document

The project MUST provide a `docs/architecture.md` file
that explains the full ecosystem: all components, their
relationships, data flows between them, and practical
decision trees for common workflows.

The document MUST include ASCII diagrams for component
relationships and specification pipeline flows.

The document MUST be written for engineers adopting
Unbound Force, not for contributors to the project.

#### Scenario: New user reads architecture overview

- **GIVEN** an engineer has run `uf init` in their project
- **WHEN** they open `docs/architecture.md`
- **THEN** they find a single document explaining all
  components (uf CLI, OpenCode, Gaze, Dewey, Replicator,
  Speckit, OpenSpec), how they connect, and when to use
  each one

#### Scenario: Architecture doc covers all components

- **GIVEN** the `docs/architecture.md` file exists
- **WHEN** a reader reviews its sections
- **THEN** they find coverage of: ecosystem overview,
  uf init scaffolding, hero team, specification pipelines,
  knowledge layer, code review, quality analysis, parallel
  execution, convention packs, artifact flow, and
  configuration

### FR-002: CLI Reference Document

The project MUST provide a `docs/cli-reference.md` file
documenting all subcommands and flags for both the `uf`
and `mutimind` CLI binaries.

Each command MUST include: command syntax, available
flags with descriptions, and a brief usage example.

#### Scenario: User looks up gateway command

- **GIVEN** a user needs to start the LLM gateway
- **WHEN** they open `docs/cli-reference.md`
- **THEN** they find `uf gateway` with its subcommands
  (start, stop, status), flags (--port, --provider,
  --detach), and a usage example

#### Scenario: User looks up mutimind command

- **GIVEN** a user needs to manage their backlog from
  the terminal
- **WHEN** they open `docs/cli-reference.md`
- **THEN** they find `mutimind` with all 12 subcommands
  documented

### FR-003: Configuration Guide

The project MUST provide a `docs/configuration.md` file
documenting the `.uf/config.yaml` configuration system.

The document MUST explain the configuration hierarchy
(project > user > defaults), all 7 configuration
sections, and common configuration scenarios.

#### Scenario: User configures Vertex AI provider

- **GIVEN** a user wants to use Vertex AI as their LLM
  provider
- **WHEN** they open `docs/configuration.md`
- **THEN** they find the `gateway` section with
  `provider: vertex` configuration and any required
  environment variables

### FR-004: Hero Capability Status Markers

The `docs/heroes.md` file MUST distinguish between
implemented and planned capabilities for each hero
using visual markers.

Implemented capabilities MUST be verifiable -- they
correspond to CLI commands or slash commands that a
user can invoke today.

#### Scenario: User checks Muti-Mind capabilities

- **GIVEN** a user reads the Muti-Mind section in
  `docs/heroes.md`
- **WHEN** they look at the capabilities list
- **THEN** they see clearly marked implemented items
  (backlog management, story generation, GitHub sync)
  and planned items (ML-based prediction, advanced
  analytics) with distinct visual markers

### FR-005: Documentation Directory Convention

Substantive documentation MUST reside in the `docs/`
directory. Root level SHOULD contain only:

- `README.md` (project overview and navigation)
- `QUICKSTART.md` (install and first use)
- `CHANGELOG.md` (change history)
- `AGENTS.md` (AI agent context)
- `CLAUDE.md` (AI tool bridge file)

#### Scenario: USAGE.md moved to docs

- **GIVEN** `USAGE.md` exists at root
- **WHEN** the documentation overhaul is applied
- **THEN** `USAGE.md` is removed from root and its
  content (expanded) exists at `docs/usage.md`
- **AND** all files that referenced `USAGE.md` link to
  `docs/usage.md` instead

#### Scenario: unbound-force.md moved and renamed

- **GIVEN** `unbound-force.md` exists at root
- **WHEN** the documentation overhaul is applied
- **THEN** `unbound-force.md` is removed from root and
  its content (cleaned) exists at `docs/heroes.md`
- **AND** all files that referenced `unbound-force.md`
  link to `docs/heroes.md` instead

### FR-010: Cross-Reference Path Updates

All agent files, command files, and their scaffold asset
copies that reference `unbound-force.md` by path MUST be
updated to reference `docs/heroes.md` instead.

The `constitution-check.md` command MUST update its
meta-repo detection heuristic to use `docs/heroes.md`
(or an equivalent sentinel) instead of
`unbound-force.md`.

Scaffold assets under `internal/scaffold/assets/` MUST
be updated in lockstep with their canonical `.opencode/`
copies to avoid drift detection test failures.

#### Scenario: Agent file references updated

- **GIVEN** `divisor-herald.md`, `divisor-envoy.md`, and
  `divisor-curator.md` previously referenced
  `unbound-force.md`
- **WHEN** the documentation overhaul is applied
- **THEN** all three agent files reference
  `docs/heroes.md` instead
- **AND** their scaffold asset copies under
  `internal/scaffold/assets/` match the updated content

#### Scenario: Constitution check detects meta repo

- **GIVEN** `unbound-force.md` no longer exists at root
- **WHEN** a user runs `/constitution-check` in the
  meta repo
- **THEN** the command detects the meta repo using the
  updated heuristic (`docs/heroes.md` or equivalent)

## MODIFIED Requirements

### FR-006: README.md Factual Accuracy

README.md MUST reflect the current state of the
repository.

Previously: README.md line 53 states "16 architectural
specifications" and line 41 uses `/opsx:propose` colon
syntax. The Repository Contents section lists only 8
items while the repo has 20+ significant entries.

The spec count MUST match the actual number of
directories in `specs/`. Command syntax
MUST use the hyphenated form (`/opsx-propose`). The
Repository Contents section MUST include all major
directories and files. Links to moved files MUST be
updated.

#### Scenario: Spec count is accurate

- **GIVEN** a user reads the README.md
- **WHEN** they see the specs/ description
- **THEN** the stated count matches the actual number
  of spec directories in `specs/`

#### Scenario: Command syntax is current

- **GIVEN** a user reads the README.md
- **WHEN** they see OpenSpec command references
- **THEN** commands use the hyphenated syntax
  (`/opsx-propose`, `/opsx-archive`) matching the
  actual command file names

### FR-007: QUICKSTART.md Completeness

QUICKSTART.md MUST provide accurate scaffolding
instructions and mention all major CLI capabilities.

Previously: Line 109 `git add` command misses `.uf/`,
`CLAUDE.md`, and `AGENTS.md`. No mention of `uf gateway`,
`uf config`, or complete `uf sandbox` capabilities.

#### Scenario: Git add after uf init is complete

- **GIVEN** a user has run `uf init`
- **WHEN** they follow the `git add` instruction in
  QUICKSTART.md
- **THEN** all scaffolded files are staged, including
  `.uf/`, `CLAUDE.md`, and `AGENTS.md` modifications

#### Scenario: User discovers gateway capability

- **GIVEN** a user reads QUICKSTART.md
- **WHEN** they look for LLM proxy setup
- **THEN** they find a mention of `uf gateway` with a
  pointer to the full CLI reference

### FR-008: Usage Guide Command Coverage

`docs/usage.md` MUST document at least 90% of available
slash commands in either the body text or the quick
reference table.

Previously: USAGE.md documented ~60% of commands. The
Divisor agent count was inconsistent ("5+" vs "9 agents").
Convention packs listing missed 3 packs (severity,
typescript, typescript-custom).

#### Scenario: Slash command discoverable in usage guide

- **GIVEN** a slash command file exists in
  `.opencode/commands/`
- **WHEN** a user opens `docs/usage.md`
- **THEN** that command appears in either a workflow
  section or the quick reference table (with the
  exception of commands that are internal implementation
  details)

### FR-009: AGENTS.md Project Structure Completeness

The AGENTS.md project structure section MUST list all
`internal/` packages.

Previously: 5 packages were missing (coaching, dashboard,
impediment, metrics, sprint). The spec count comment
(`001-018`) is stale (actual: `001-035`). The `docs/`
directory is not listed.

#### Scenario: All internal packages listed

- **GIVEN** a developer reads the AGENTS.md project
  structure
- **WHEN** they look at the `internal/` listing
- **THEN** all packages are listed with one-line
  descriptions matching the actual directory count

#### Scenario: Spec count and docs directory listed

- **GIVEN** a developer reads the AGENTS.md project
  structure
- **WHEN** they look at the `specs/` entry
- **THEN** the comment matches the actual spec range
- **AND** a `docs/` entry exists with a description

## REMOVED Requirements

None. No existing requirements are removed by this
change.
