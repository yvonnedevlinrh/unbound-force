## Why

Unbound Force has grown significantly -- 35 architectural
specs, 18 agents, ~40 slash commands, 7 CLI subcommands,
and 5 interconnected external tools (Gaze, Dewey,
Replicator, Speckit, OpenSpec). Adoption is increasing,
but the documentation has not kept pace.

New engineers face three problems:

1. **No architecture overview** -- There is no document
   explaining how the components connect, what data flows
   between them, or why the system is designed this way.
   Users must piece this together from README, QUICKSTART,
   USAGE, AGENTS.md, and 35 specs.

2. **Stale and incomplete docs** -- README claims 16 specs
   (actual: 35), uses deprecated colon syntax for commands,
   and lists only 1 of 16 internal packages. QUICKSTART has
   an incomplete `git add` command. USAGE covers only ~60%
   of slash commands and 0% of CLI subcommands. Major
   features (`uf gateway`, `uf config`, `uf sandbox`,
   `mutimind` CLI) have zero user-facing documentation.

3. **File sprawl** -- 7 markdown files at root, but no
   `docs/` directory exists on `main` (one is introduced
   on the unmerged `opsx/release-automation` branch).
   `unbound-force.md` is a 151-line design charter
   misnamed as if it were the project overview.

The goal is clear, simple, and effective documentation
that accelerates onboarding for engineers adopting
Unbound Force and AI Native Development workflows.

## What Changes

### Documentation reorganization

- Move `USAGE.md` to `docs/usage.md` (expand with
  missing commands and CLI reference sections)
- Move `unbound-force.md` to `docs/heroes.md` (rename
  to reflect actual content, fix typos, add
  implemented-vs-planned capability markers)
- Keep `README.md`, `QUICKSTART.md`, `CHANGELOG.md`,
  `AGENTS.md`, `CLAUDE.md` at root (entry points and
  AI context files)

### New documentation

- `docs/architecture.md` -- The centerpiece: ecosystem
  diagram, component relationships, artifact flow,
  specification pipelines, knowledge layer, convention
  packs, configuration hierarchy, and practical examples
- `docs/cli-reference.md` -- Full `uf` and `mutimind`
  command trees with flags, subcommands, and examples
- `docs/configuration.md` -- Guide to `.uf/config.yaml`
  with all 7 sections, defaults, and common scenarios

### Existing doc fixes

- README.md: fix spec count (16 → 35), fix colon syntax
  (`/opsx:propose` → `/opsx-propose`), update repository
  contents section, update links to moved files
- QUICKSTART.md: fix incomplete `git add`, add mentions
  of gateway/config/sandbox, add scaffolded files summary
- USAGE.md (before move): fix Divisor count inconsistency
  ("5+" vs "9"), add ~15 undocumented slash commands, add
  CLI subcommand sections, update convention packs listing
- AGENTS.md: add 5 missing internal packages (coaching,
  dashboard, impediment, metrics, sprint), fix stale
  spec count (001-018 → 001-035), add docs/ entry
- heroes.md (after move): fix typos, remove stale Swarm
  plugin reference, add per-hero capability status markers
- Agent and command file path updates: 3 agent files
  and 1 command file reference `unbound-force.md` by
  path, plus their 4 scaffold asset copies in
  `internal/scaffold/assets/` — all 8 need path updates
  to `docs/heroes.md`
- CHANGELOG.md: add entry for this documentation overhaul

## Capabilities

### New Capabilities

- `docs/architecture.md`: Single document explaining the
  full ecosystem -- components, connections, data flows,
  specification pipelines, and practical decision trees
- `docs/cli-reference.md`: Complete CLI reference for
  both `uf` (7 commands, 20+ subcommands) and `mutimind`
  (12 subcommands)
- `docs/configuration.md`: Configuration guide covering
  the layered hierarchy and all 7 config sections

### Modified Capabilities

- `docs/usage.md`: Expanded from ~60% to ~95% command
  coverage, adds CLI subcommand documentation, fixes
  inconsistencies
- `docs/heroes.md`: Cleaned hero descriptions with
  implemented-vs-planned markers per hero
- `README.md`: Accurate repository contents, correct
  links, current spec count
- `QUICKSTART.md`: Complete scaffolding instructions,
  mentions all major CLI features
- `AGENTS.md`: Complete internal package listing

### Removed Capabilities

- `USAGE.md` (root): Replaced by `docs/usage.md`
- `unbound-force.md` (root): Replaced by `docs/heroes.md`

## Impact

### Affected files

- `README.md` -- content fixes and link updates
- `QUICKSTART.md` -- content fixes and additions
- `USAGE.md` -- moved to `docs/usage.md`, expanded
- `unbound-force.md` -- moved to `docs/heroes.md`,
  cleaned
- `AGENTS.md` -- project structure section updated
- `CHANGELOG.md` -- change entry added
- `docs/architecture.md` -- new file
- `docs/cli-reference.md` -- new file
- `docs/configuration.md` -- new file
- `.opencode/agents/divisor-herald.md` -- path update
- `.opencode/agents/divisor-envoy.md` -- path update
- `.opencode/agents/divisor-curator.md` -- path update
- `.opencode/commands/constitution-check.md` -- path
  update (meta-repo detection heuristic)
- `internal/scaffold/assets/opencode/agents/divisor-herald.md`
- `internal/scaffold/assets/opencode/agents/divisor-envoy.md`
- `internal/scaffold/assets/opencode/agents/divisor-curator.md`
- `internal/scaffold/assets/opencode/commands/constitution-check.md`

### Scope note

No Go source code, convention packs, or CI
configuration are modified. Agent files, command files,
and their scaffold asset copies require path reference
updates (not content rewrites) to reflect the move of
`unbound-force.md` to `docs/heroes.md`. Scaffold assets
under `internal/scaffold/assets/` are embedded via
Go `embed.FS` — changes trigger existing drift
detection tests.

### Cross-reference impact

Any file referencing `USAGE.md` or `unbound-force.md`
by path needs updated links. This includes README.md,
QUICKSTART.md, 3 agent files, 1 command file, and
their 4 scaffold asset copies.

## Constitution Alignment

Assessed against the Unbound Force org constitution.

### I. Autonomous Collaboration

**Assessment**: N/A

This change modifies documentation only. No hero
artifacts, inter-hero communication protocols, or
artifact envelope formats are affected.

### II. Composability First

**Assessment**: N/A

No hero functionality is modified. Documentation
improvements do not affect standalone installability
or inter-hero dependencies.

### III. Observable Quality

**Assessment**: PASS

This change improves the observability of the system
by documenting previously undocumented capabilities
(gateway, config, sandbox, mutimind CLI). It makes
the architecture visible through diagrams and
component relationship maps. No machine-parseable
outputs or provenance metadata are affected.

### IV. Testability

**Assessment**: PASS

New documentation files do not require test coverage.
However, scaffold assets under `internal/scaffold/assets/`
are modified (path reference updates) and are covered by
existing drift detection tests
(`TestEmbeddedAssets_MatchSource`) that verify embedded
assets match their canonical sources.
