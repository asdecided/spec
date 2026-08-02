# Changelog

Changes to the RAC (Requirements as Code) specification, by version. The
specification versions independently of any implementation, on semantic
versioning; the compatibility rules are in SPEC.md §10.2.

## Unreleased

- **Deterministic code constraints** — decision artifacts may carry a
  versioned `## Code Constraints` YAML block with `forbid_pattern`,
  `require_pattern`, and `forbid_import` rules. §8.7 specifies diff and
  full-tree enforcement, deterministic execution, explicit unsupported-
  language failures, and published decision-coverage counts. No model or
  probabilistic judge is permitted. `schema/code-constraints.schema.json`
  is the language-neutral machine contract.
- **Repository identity** — moved the repository to `asdecided/spec` and
  updated reference-implementation links to `asdecided/core`. The stable RAC
  vocabulary, artifact IDs, schema keys, and conformance contracts are
  unchanged.
- **mcp/conformance/vectors.json** and **mcp/README.md** — the first
  language-neutral MCP compatibility surface: current 2026-07-28 semantic
  vectors, explicitly frozen legacy bytes, JSON-RPC envelope and metadata
  negatives, HTTP version-carrier and Origin outcomes, notifications, and
  tool-schema object-root assertions. The fixtures are implementation-neutral
  and do not depend on a Python oracle.
- **conformance/output-parity.json**, **conformance/vectors/** — the
  output-parity conformance tier (asdecided-core ADR-063 Guard 2): eleven cases,
  each pinning the byte-for-byte stdout (with sha256) and exit code of a
  deterministic, recency-free command over the example corpora. The goldens
  are the reference implementation's exact output; an implementation claiming
  this tier must reproduce every case exactly. Optional tier; producer/
  consumer conformance is unchanged.
- **schema/artifact-specs.json** — the canonical machine-readable
  artifact-spec registry (ordered artifact specs with section tiers, metadata
  enums, descriptions, guidance, synonyms, and starter bodies, plus
  relationship-section descriptions). This file is a source of truth engines
  read, not derived documentation: the native reference implementation
  vendors it for its Rust engine, with a sync gate holding the copies
  identical (asdecided-core ADR-115, ADR-063 Guard 1).
  Additive; no normative statement in SPEC.md changes.

## v0.1.0 — 2026-07-05

Initial extraction of the specification from the reference implementation,
[`asdecided-core`](https://github.com/asdecided/core).

- **SPEC.md** — the normative specification: artifact model (five types,
  frontmatter envelope, ID grammar and path-independent identity, per-type
  sections, requirement-line grammar), the closed `status` lifecycle with
  supersession semantics, the closed typed-relationship vocabulary with
  referential integrity and graph-shape rules, the finding/severity/
  enforcement model with the normative check table, conformance levels, the
  versioning and compatibility policy, and the OKF composition contract.
- **schema/** — machine-readable JSON Schemas for the frontmatter envelope
  and the parsed per-type structural contract.
- **vocabulary/** — the closed `status` and relationship enums as tables.
- **conformance/** — conformant/gated corpus and producer/consumer
  definitions, plus the OKF-consumer compatibility note.
- **examples/** — the Appendix A minimal corpus, one valid artifact per
  type, and one annotated invalid case per major rule, indexed by
  `manifest.json` as an executable acceptance suite.

One deliberate forward-looking addition beyond extraction-time validator
behavior: the corpus-level spec-version declaration (`rac_spec` in
`.rac/config.yaml`, SPEC.md §10.1). The reference implementation is committed
to reading it — and refusing newer-versioned corpora per §10.3 — before the
v0.1.0 announcement; SPEC.md §10.1 carries the status note.
