# ADR-002: Use Explicit Schema Contracts

## Status

Accepted

---

## Context

Pipeline validation requirements were previously embedded inside execution logic.

This creates several problems:

- Validation rules duplicated across pipelines
- Difficult testing
- Difficult governance
- Inconsistent behavior

The platform requires a standardized validation mechanism.

---

## Decision

Introduce Schema Contracts as independent components.

Each pipeline references a schema contract.

Schema contracts define:

- Required fields
- Datatypes
- Allowed values
- Default values
- Validation rules

---

## Rationale

Separating validation from execution provides:

- Reusability
- Consistency
- Easier governance
- Better testing

Validation becomes declarative rather than procedural.

---

## Example

Pipeline:

```text
customer_daily
```

References:

```text
schema_customer_load_v1
```

The schema contract performs validation before execution begins.

---

## Consequences

### Positive

- Centralized validation
- Consistent behavior
- Easier maintenance
- Better compliance

### Negative

- Additional component management
- Version compatibility considerations

---

## Alternatives Considered

### Validation Embedded In Templates

Rejected because logic becomes duplicated.

### Validation Embedded In Pipelines

Rejected because governance becomes difficult.

---

## Result

Validation becomes reusable, governed, and independently maintained.
