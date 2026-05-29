# ADR-001: Adopt Reference-Based Pipeline Architecture

## Status

Accepted

---

## Context

The legacy metadata-driven framework stores pipeline identity, execution logic, validation rules, scheduling information, and runtime configuration within a tightly coupled structure.

As the number of pipelines grows, the framework becomes increasingly difficult to maintain because:

- Changes affect multiple pipelines
- Logic is duplicated
- Validation rules are inconsistent
- Deployment risk increases
- Ownership boundaries are unclear

The platform requires a more scalable and maintainable architecture.

---

## Decision

Adopt a Reference-Based Pipeline Architecture.

Instead of embedding all behavior inside a single metadata structure, pipelines become compositions of independently managed components connected through explicit references.

A pipeline will reference:

- Schema Contract
- Pipeline Template
- Orchestration Definition
- Runtime Parameters

---

## Rationale

This design promotes:

- Loose coupling
- High cohesion
- Reuse
- Governance
- Independent evolution

Each component can change without requiring platform-wide modifications.

---

## Consequences

### Positive

- Easier maintenance
- Better governance
- Safer deployments
- Reduced regression risk
- Improved scalability

### Negative

- Additional metadata structures
- More initial design effort
- Dependency management required

---

## Alternatives Considered

### Continue Existing Framework

Rejected because coupling continues to increase.

### Fully Dynamic Runtime Assembly

Rejected because operational complexity increases significantly.

---

## Result

Pipeline behavior becomes composable, reusable, and independently governed.
