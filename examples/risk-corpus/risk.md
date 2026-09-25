---
schema_version: 1
id: EX-0000000000K2
type: risk
---
# Queue vendor lock-in

## Status

Accepted

## Risk

Moving off the managed queue later would touch every producer and consumer.

## Likelihood

Moderate: the vendor has changed pricing twice in two years.

## Impact

A migration would take one team a quarter, and order processing would run on
two queues while it happens.

## Context

ADR-001 adopted a managed queue for order events.

## Assumptions

- Order volume stays within the vendor's standard tier.

## Mitigation

Producers publish through one adapter, so a move changes one module rather
than every service.

## Related Decisions

- EX-0000000000K1
