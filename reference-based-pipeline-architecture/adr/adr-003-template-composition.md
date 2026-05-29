# ADR-003: Separate Pipeline Templates From Configuration

## Status

Accepted

---

## Context

Traditional pipeline frameworks often combine:

- Execution logic
- Configuration
- Runtime values

inside a single structure.

This creates duplication because similar execution patterns are implemented repeatedly.

Examples:

- Full load
- Incremental load
- Merge load
- CDC load

The execution logic is often identical while only configuration differs.

---

## Decision

Separate execution templates from runtime configuration.

Pipeline Templates define:

- Execution flow
- Processing stages
- Control logic

Runtime Parameters define:

- Source tables
- Target tables
- Load dates
- Environment settings

Pipelines reference templates rather than embedding execution logic.

---

## Rationale

Templates become reusable across many pipelines.

A single template can support hundreds of pipelines through different parameter sets.

---

## Example

Template:

```text
incremental_load_template
```

Pipeline A:

```text
customer_daily
```

Pipeline B:

```text
orders_daily
```

Both reference the same template.

---

## Consequences

### Positive

- Massive reduction in duplication
- Easier maintenance
- Faster onboarding
- Consistent execution behavior

### Negative

- Template versioning required
- Dependency tracking required

---

## Alternatives Considered

### Template Per Pipeline

Rejected because duplication grows rapidly.

### Fully Dynamic Execution Engine

Rejected because complexity outweighs benefits.

---

## Result

Execution logic becomes reusable, standardized, and independently governed from runtime configuration.
