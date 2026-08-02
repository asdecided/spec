# MCP compatibility fixtures

This directory is the language-neutral compatibility surface for the AsDecided
MCP server. It is intentionally separate from the RAC artifact conformance
examples: RAC describes the corpus; these vectors describe the wire contract
of an MCP implementation serving that corpus.

The authoritative manifest is [`conformance/vectors.json`](conformance/vectors.json).
It is a small, versioned JSON document with no implementation-specific paths,
timestamps, or model calls. A vector contains:

- `transport`: `stdio` or `http`;
- `request`: one JSON-RPC request object;
- `http` (HTTP vectors only): request headers, path, optional allow-list, and
  an optional declared `content_length` used to exercise framing policy;
- `expect`: either exact legacy frames or schema-constrained assertions.

Assertions use JSON Pointer. `equals` pins a scalar/object value, `exists`
requires a field to be present, and `absent` requires it not to be present.
Current-protocol vectors use assertions so an implementation can choose its
own package version and audit path. The legacy vector set is explicitly
byte-oriented: frozen 2025 behavior is represented by `exact_frames` and must
not be silently normalized into current semantics.

The vectors cover the MCP 2026-07-28 discovery and metadata contract, current
result typing and cache hints, JSON-RPC envelope validity, notifications and
IDs, legacy initialization, HTTP version-carrier agreement, Origin policy,
structured errors, and tool-schema object roots. They are protocol fixtures,
not a Python oracle: a future implementation reads the same JSON and runs its
own transport adapter.

The format is deliberately additive. New vectors MUST have stable IDs and MUST
avoid asserting incidental fields such as timestamps, temporary paths, or
implementation package versions. Changes to a frozen legacy frame require a
reviewed compatibility decision; changes to current semantic assertions are
documented in [`CHANGELOG.md`](../CHANGELOG.md).

The current vectors target the official
[MCP 2026-07-28 specification](https://modelcontextprotocol.io/specification/2026-07-28)
and AsDecided's declared dual-era compatibility policy. They do not replace
the official specification; they make the subset AsDecided ships executable
and portable across implementations.
