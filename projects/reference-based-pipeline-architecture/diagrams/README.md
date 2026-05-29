# Architecture Diagrams

This folder contains architecture diagrams supporting the Reference-Based Pipeline Architecture project.

The diagrams illustrate how pipeline identity, structure, validation, orchestration, and configuration are separated into independently managed components connected through explicit references.

---

## Diagram Index

### architecture.png

High-level architecture of the reference-based pipeline framework.

Shows:

- Pipeline Registry
- Parameter Schema
- Pipeline Template
- Parameter Values
- Pipeline Orchestration

Purpose:

Provide an executive-level view of the overall system design.

---

### component-model.png

Logical component model showing responsibilities and boundaries.

Shows:

- Ownership of each component
- Reference relationships
- Separation of concerns
- Dependency boundaries

Purpose:

Demonstrate low coupling and high cohesion.

---

### execution-flow.png

Runtime execution sequence.

Shows:

```text
pipeline_id
    |
    v
resolve schema contract
    |
    v
resolve template
    |
    v
load parameters
    |
    v
validate
    |
    v
build execution plan
    |
    v
execute
