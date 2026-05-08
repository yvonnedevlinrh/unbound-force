<!--
  [P] marks tasks eligible for parallel execution.
  Add [P] when a task: (a) touches different files from
  other [P] tasks in the group, (b) has no dependency
  on prior tasks in the group, (c) can safely execute
  without ordering constraints.
  Do NOT add [P] when tasks modify the same file —
  parallel workers will cause merge conflicts.
  Tasks without [P] run sequentially first, then [P]
  tasks run in parallel.
-->

## 1. Create New Documentation Files

- [x] 1.1 [P] Create `docs/architecture.md` with
  ecosystem overview diagram (all components and
  connections), what `uf init` does (scaffolded files,
  ownership model, bridge files, sub-tool delegation),
  hero team table with current capabilities, specification
  pipelines (Speckit vs OpenSpec with decision tree and
  command-to-artifact flow), knowledge layer (Dewey
  indexing, agent queries, 3-tier degradation), code
  review (Divisor council model, 9 personas, convention
  packs), quality analysis (Gaze CRAP scores, test
  generation), parallel execution (forge coordinator/worker
  model, file reservations), convention pack system
  (tool-owned vs custom, consumers), artifact flow
  (hero-to-hero communication, well-known paths), and
  configuration (hierarchy, key sections, examples).
  Use ASCII diagrams for component relationships and
  pipeline flows. Ensure the `docs/` directory is
  created if it does not exist. FR-001.
  Files: `docs/architecture.md`

- [x] 1.2 [P] Create `docs/cli-reference.md` with full
  command trees for `uf` (init, version, doctor, setup,
  sandbox, gateway, config — all subcommands and flags)
  and `mutimind` (init, add, list, update, show,
  sync-push, sync-pull, sync-status, sync, sync-project,
  generate-artifact, decide). Include command syntax,
  flag descriptions, and brief usage examples for each
  command. FR-002.
  Files: `docs/cli-reference.md`

- [x] 1.3 [P] Create `docs/configuration.md` explaining
  the `.uf/config.yaml` system: configuration hierarchy
  (CLI flags > env vars > repo config > user config >
  compiled defaults), all 7 sections (scaffold, doctor,
  setup, sandbox, gateway, embedding, workflow) with
  their fields, defaults, and types. Include common
  scenarios: Vertex AI setup, skipping tools in setup,
  sandbox resource limits, custom embedding model.
  FR-003.
  Files: `docs/configuration.md`

## 2. Move and Clean Existing Files

- [x] 2.1 [P] Move `unbound-force.md` to `docs/heroes.md`
  using `git mv`. Fix typos ("heros" → "heroes",
  "The can be" → "They can be"). Remove stale Swarm
  plugin reference at swarmtools.ai (now built-in
  forge/orchestration). Update Overview paragraph for
  accuracy. Add per-hero Current Capabilities vs Planned
  sections with visual markers. Muti-Mind implemented:
  backlog CRUD, story generation, GitHub issue sync,
  acceptance decisions, artifact generation. Muti-Mind
  planned: advanced analytics, ML-based prediction.
  Gaze implemented: CRAP scores, coverage metrics, test
  generation, side effect classification. Gaze planned:
  ML-based risk prediction, load/stress testing.
  Cobalt-Crush implemented: developer agent persona,
  convention pack adherence, Speckit/OpenSpec
  implementation, Gaze feedback loop. The Divisor
  implemented: 9-persona council (guard, architect,
  adversary, sre, testing, curator, scribe, herald,
  envoy), convention packs, dynamic discovery. Mx F
  implemented: coaching agent, retrospective
  facilitation, metrics collection, dashboard rendering,
  impediment tracking, sprint management. Mx F planned:
  capacity prediction, burnout detection. FR-004, FR-005.
  Files: `docs/heroes.md`, `unbound-force.md`

- [x] 2.2 [P] Move `USAGE.md` to `docs/usage.md` using
  `git mv`. Fix Divisor count inconsistency (line 52
  "5+" → match "9 agents" on line 35). Add
  `/opsx-explore` to body text (currently only in quick
  reference). Update convention packs listing to include
  `severity.md`, `typescript.md`, `typescript-custom.md`.
  Add missing slash commands to quick reference:
  `/review-pr`, `/agent-brief`, `/org`, `/handoff`,
  `/inbox`, `/forge`, `/forge-status`, `/uf-init`,
  `/constitution-check`, `/workflow-start`,
  `/workflow-status`, `/workflow-advance`,
  `/workflow-list`, `/workflow-seed`,
  `/speckit.constitution`, `/speckit.analyze`,
  `/speckit.checklist`, `/speckit.taskstoissues`,
  `/speckit.testreview`. Add "CLI Commands" section
  referencing `docs/cli-reference.md` for terminal
  usage (depends on 1.2 existing). FR-005, FR-008.
  Files: `docs/usage.md`, `USAGE.md`

## 3. Fix Existing Documentation

- [x] 3.1 [P] Fix `README.md`: update spec count to
  match actual directory count in `specs/` (currently
  35). Fix `/opsx:propose` and `/opsx:archive` to
  `/opsx-propose` and `/opsx-archive` (line 41). Add
  `cmd/mutimind/` to Repository Contents. Update
  Repository Contents to include `docs/`, `schemas/`,
  `.opencode/`. Update link from `USAGE.md` to
  `docs/usage.md`. Update link from `unbound-force.md`
  to `docs/heroes.md`. Add links to new docs
  (architecture, cli-reference, configuration). FR-006.
  Files: `README.md`

- [x] 3.2 [P] Fix `QUICKSTART.md`: update `git add`
  on line 109 to include `.uf/`, `CLAUDE.md`, and note
  that `AGENTS.md` may be modified. Add brief mentions
  of `uf gateway` (for Vertex/Bedrock users), `uf config`
  (for customization), and `uf sandbox` (full capability
  overview). Add a "What Gets Scaffolded" summary after
  the `uf init` section explaining what the 34+ files
  are (agents, commands, convention packs, OpenSpec
  schema, skills). Update "Next Steps" link from
  `USAGE.md` to `docs/usage.md`. FR-007.
  Files: `QUICKSTART.md`

- [x] 3.3 [P] Fix `AGENTS.md`: add 5 missing internal
  packages to the project structure section: `coaching/`
  (Mx F coaching and retrospective data), `dashboard/`
  (Mx F dashboard rendering), `impediment/` (Impediment
  tracking and detection), `metrics/` (Metrics collection
  and health analysis), `sprint/` (Sprint lifecycle
  management). Fix stale spec count comment from
  `(001-018)` to match actual range. Add `docs/` entry
  to project structure (user-facing documentation).
  Match the existing one-line comment format. FR-009.
  Files: `AGENTS.md`

## 4. Update Cross-References in Agent and Command Files

- [x] 4.1 [P] Update `unbound-force.md` references to
  `docs/heroes.md` in `.opencode/agents/divisor-herald.md`
  and its scaffold copy at
  `internal/scaffold/assets/opencode/agents/divisor-herald.md`.
  FR-010.
  Files: `.opencode/agents/divisor-herald.md`,
  `internal/scaffold/assets/opencode/agents/divisor-herald.md`

- [x] 4.2 [P] Update `unbound-force.md` references to
  `docs/heroes.md` in `.opencode/agents/divisor-envoy.md`
  and its scaffold copy at
  `internal/scaffold/assets/opencode/agents/divisor-envoy.md`.
  FR-010.
  Files: `.opencode/agents/divisor-envoy.md`,
  `internal/scaffold/assets/opencode/agents/divisor-envoy.md`

- [x] 4.3 [P] Update `unbound-force.md` references to
  `docs/heroes.md` in
  `.opencode/agents/divisor-curator.md` and its scaffold
  copy at
  `internal/scaffold/assets/opencode/agents/divisor-curator.md`.
  FR-010.
  Files: `.opencode/agents/divisor-curator.md`,
  `internal/scaffold/assets/opencode/agents/divisor-curator.md`

- [x] 4.4 [P] Update the meta-repo detection heuristic
  in `.opencode/commands/constitution-check.md` from
  checking for `unbound-force.md` to checking for
  `docs/heroes.md`. Update its scaffold copy at
  `internal/scaffold/assets/opencode/commands/constitution-check.md`.
  FR-010.
  Files: `.opencode/commands/constitution-check.md`,
  `internal/scaffold/assets/opencode/commands/constitution-check.md`

## 5. Finalize

- [x] 5.1 Add `CHANGELOG.md` entry for the
  documentation-overhaul change summarizing: file moves
  (USAGE.md → docs/usage.md, unbound-force.md →
  docs/heroes.md), new docs created (architecture,
  cli-reference, configuration), existing doc fixes
  (README, QUICKSTART, AGENTS.md), and agent/command
  file path updates.
  Files: `CHANGELOG.md`

## 6. Verification

- [x] 6.1 Verify cross-references: grep recursively
  across the entire repository for any remaining
  references to `USAGE.md` or `unbound-force.md` in
  all markdown files (including `.opencode/`,
  `internal/scaffold/assets/`, and `specs/`). Historical
  references in `specs/` completed tasks and changelogs
  are acceptable. Active references in `.opencode/` and
  `internal/scaffold/` files must all point to new
  locations. Verify README.md links to
  `docs/usage.md`, `docs/heroes.md`,
  `docs/architecture.md`, `docs/cli-reference.md`,
  and `docs/configuration.md` are correct.

- [x] 6.2 Verify constitution alignment: confirm
  Principle I (Autonomous Collaboration) N/A — no hero
  artifacts modified. Principle II (Composability) N/A —
  no hero dependencies changed. Principle III
  (Observable Quality) PASS — previously undocumented
  capabilities now documented. Principle IV
  (Testability) PASS — scaffold asset drift detection
  tests cover embedded file changes.

- [x] 6.3 Verify documentation completeness: confirm
  `docs/` contains architecture.md, usage.md,
  heroes.md, cli-reference.md, and configuration.md.
  Confirm root level has only README.md, QUICKSTART.md,
  CHANGELOG.md, AGENTS.md, and CLAUDE.md as markdown
  files. Confirm `unbound-force.md` and `USAGE.md` no
  longer exist at root.
<!-- spec-review: passed -->
<!-- code-review: passed -->
