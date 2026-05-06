## Context

The project has 7 markdown files at root level and no
`docs/` directory on `main` (one is introduced on the
unmerged `opsx/release-automation` branch with
`RELEASE_PROCESS.md`).
Documentation has not kept pace with implementation --
major features are undocumented, factual errors exist in
published docs, and there is no single document explaining
how the ecosystem's components connect.

The target audience is engineers adopting Unbound Force in
their projects and practitioners of AI Native Development.
They need to understand what UF gives them, how tools
relate, and how to use the system effectively.

## Goals / Non-Goals

### Goals

- Provide a single architecture document that explains
  all components and their relationships
- Fix all known factual errors in existing documentation
- Establish `docs/` as the canonical documentation home
- Document all CLI commands (uf and mutimind) with
  reference material
- Document the configuration system
- Clearly distinguish implemented vs planned capabilities
  in hero descriptions
- Expand slash command coverage from ~60% to ~95%

### Non-Goals

- Rewriting agent persona content or behavior
- Modifying convention pack rules or command logic
  (note: mechanical path reference updates in agent
  and command files ARE in scope per D7)
- Adding automated documentation generation or tooling
- Creating a documentation website (that is the
  unbound-force/website repo's responsibility)
- Documenting internal Go package APIs (godoc handles
  that)
- Modifying AGENTS.md beyond the project structure
  section (it serves AI agents, not human onboarding)

## Decisions

### D1: Keep QUICKSTART.md at root

QUICKSTART.md stays at root for GitHub discoverability.
When someone visits the repo, GitHub renders README.md
which links to QUICKSTART.md. Moving it to `docs/` adds
a click and reduces the chance a new user finds it.

USAGE.md moves to `docs/` because it is a reference
document, not an entry point. The README links to it
explicitly, so discoverability is preserved through the
link rather than filesystem proximity.

### D2: Rename unbound-force.md to docs/heroes.md

The current name `unbound-force.md` collides with the
project name and gives no hint about its content (hero
role descriptions). `heroes.md` matches the project
vocabulary ("heroes" is used throughout the codebase,
agents, and specs) and accurately describes the content.

It moves to `docs/` because it is reference material,
not an entry point.

### D3: architecture.md structure follows user journey

The architecture document is ordered by what a new user
needs to understand first:

1. Ecosystem overview (the map)
2. What uf init does (what they just ran)
3. The heroes (who does what)
4. Specification pipelines (how work flows)
5. Knowledge layer, review, quality (supporting systems)
6. Parallel execution (advanced topic)
7. Convention packs, artifacts, config (customization)

This is deliberately not organized by internal package
structure. Users think in workflows, not packages.

### D4: Implemented vs planned capability markers

Hero descriptions in `docs/heroes.md` use a two-layer
approach:

```
**Vision**: <charter language, 2-3 sentences>

**Current Capabilities**:
- Backlog management (add, list, update, prioritize)
- User story generation from goals
- GitHub issue sync (bidirectional)
- Acceptance decisions via artifacts

**Planned**:
- Advanced analytics and market intelligence
- ML-based risk prediction
```

The vision stays for directional context. The capability
list tells the truth. No capability is listed without a
marker indicating its status. This prevents the trust
erosion that occurs when users try to use features that
are described but not implemented.

### D5: Separate CLI reference from usage guide

`docs/usage.md` covers workflows and slash commands
(the OpenCode experience). `docs/cli-reference.md`
covers the terminal CLI (`uf` and `mutimind` binaries).

These are different interaction surfaces:
- Slash commands run inside OpenCode sessions
- CLI commands run in the terminal

Mixing them in one document would confuse the mental
model. A user asking "how do I configure my gateway"
goes to cli-reference. A user asking "how do I review
code" goes to usage.

### D6: docs/ directory as canonical documentation home

All substantive documentation lives in `docs/`. Root
level retains only:

- `README.md` -- project overview and navigation hub
- `QUICKSTART.md` -- install and first 5 minutes (D1)
- `CHANGELOG.md` -- change history (conventional)
- `AGENTS.md` -- AI agent context (not user docs)
- `CLAUDE.md` -- bridge file (not user docs)

This follows the convention that root-level files are
either GitHub-conventional (README, CHANGELOG) or tool
configuration (AGENTS, CLAUDE). Documentation lives in
`docs/`.

### D7: Cross-reference strategy

When files move, all references update in the same
change. A repository-wide grep identifies all files
referencing the moved paths:

- `USAGE.md` -- referenced by README.md, QUICKSTART.md
- `unbound-force.md` -- referenced by README.md,
  `.opencode/agents/divisor-herald.md` (source doc),
  `.opencode/agents/divisor-envoy.md` (source doc),
  `.opencode/agents/divisor-curator.md` (path heuristic),
  `.opencode/commands/constitution-check.md` (meta-repo
  detection sentinel)

Each of these also has a scaffold asset copy under
`internal/scaffold/assets/` that must be updated in
lockstep to avoid drift detection test failures.

The `constitution-check.md` command uses the existence
of `unbound-force.md` at root as a heuristic to detect
the meta repo. After the move, this heuristic is updated
to check for `docs/heroes.md` instead.

Convention packs do not reference these files.

### D8: AGENTS.md project structure update

Five internal packages are missing from the AGENTS.md
project structure section: `coaching/`, `dashboard/`,
`impediment/`, `metrics/`, `sprint/`. These are all
Mx F subsystem packages. They are added with one-line
descriptions matching the established format.

## Risks / Trade-offs

### R1: Documentation drift after this change

New documentation requires maintenance. Mitigation:
the `/agent-brief` command already audits AGENTS.md
for structural completeness. A future enhancement could
extend its checks to `docs/` files, but that is out of
scope for this change.

### R2: Moved files break external links

If anyone has bookmarked or linked to the GitHub URLs
for `USAGE.md` or `unbound-force.md` at root, those
links break. Mitigation: GitHub does not support
redirects for moved files. The README.md navigation
hub is the stable entry point and will have correct
links after this change. The risk is low given the
project's current adoption stage.

### R3: Architecture doc may become stale

The architecture document describes the current state
of interconnected tools. As tools evolve, sections may
become inaccurate. Mitigation: the document is written
at a conceptual level (component relationships, data
flow patterns) rather than implementation detail level.
Conceptual architecture changes less frequently than
implementation details.

### R5: Scaffold asset drift detection

Modifying agent files in `.opencode/agents/` requires
updating their embedded copies in
`internal/scaffold/assets/`. The project has a drift
detection test (`TestEmbeddedAssets_MatchSource`) that
fails if these diverge. Mitigation: the task list
explicitly includes both live and scaffold copies for
each affected agent and command file.

### R4: Aspirational content judgment calls

Deciding what is "implemented" vs "planned" for hero
capabilities requires judgment. Some features are
partially implemented (e.g., Mx F has metrics collection
but not ML-based prediction). Mitigation: capabilities
are marked as implemented only if a user can invoke them
today through CLI or slash commands. Internal packages
that exist but are not exposed through user-facing
interfaces are noted but not listed as user capabilities.
