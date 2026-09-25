---
schema_version: 1
id: EX-0000000000K1
type: decision
---
# ADR-001: Use a managed message queue

## Status

Accepted

## Context

Orders are lost when the in-process queue restarts.

## Decision

Adopt a managed, durable message queue for order events.

## Consequences

Order events survive restarts; the service now depends on one queue vendor.

## Related Requirements

- EX-0000000000K3

## Related Risks

- EX-0000000000K2
