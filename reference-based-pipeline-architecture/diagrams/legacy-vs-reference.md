# Legacy vs Reference-Based Architecture

## Purpose

This diagram compares a traditional monolithic metadata-driven architecture with the proposed Reference-Based Pipeline Architecture.

The objective is to demonstrate how separating responsibilities into independently managed components improves maintainability, scalability, governance, testing, operational transparency, and long-term platform evolution.

---

## Legacy Metadata-Driven Architecture

```text
                          LEGACY ARCHITECTURE

                   +----------------------------------+
                   |       METADATA CONFIG TABLE      |
                   |                                  |
                   |  Pipeline Definitions            |
                   |  Runtime Parameters              |
                   |  Validation Rules                |
                   |  Execution Logic                 |
                   |  Scheduling Information          |
                   |  Environment Settings            |
                   |  Data Quality Rules              |
                   |  Business Rules                  |
                   +---------------+------------------+
                                   |
                                   |
                                   v

                     +----------------------------+
                     |     EXECUTION ENGINE       |
                     +----------------------------+
                                   |
                                   v

                     +----------------------------+
                     |      PIPELINE RUN          |
                     +----------------------------+
```

---

## Problems with Legacy Architecture

### Excessive Coupling

Pipeline identity, execution logic, scheduling, validation, and runtime configuration are tightly bound together.

### Large Blast Radius

A change to a shared metadata structure can impact many pipelines simultaneously.

### Difficult Extension

Adding new pipeline patterns often requires modifying existing framework logic.

### Reduced Reusability

Business logic, validation, and orchestration become duplicated across pipelines.

### Governance Challenges

Ownership boundaries are unclear because responsibilities overlap.

### Operational Complexity

Troubleshooting requires understanding a large centralized configuration structure.

---

## Reference-Based Architecture

```text
                    REFERENCE-BASED ARCHITECTURE

                       +----------------------+
                       |  PIPELINE REGISTRY   |
                       |  Identity Catalog    |
                       +----------+-----------+
                                  |
                                  |
              +-------------------+-------------------+
              |                   |                   |
              v                   v                   v

      +---------------+   +---------------+   +---------------+
      | Schema        |   | Pipeline      |   | Orchestration |
      | Contract      |   | Template      |   | Definition    |
      +---------------+   +---------------+   +---------------+

                                  |
                                  v

                     +--------------------------+
                     |    Parameter Values      |
                     |    Runtime Configuration |
                     +--------------------------+

                                  |
                                  v

                     +--------------------------+
                     |      Execution Plan      |
                     +--------------------------+

                                  |
                                  v

                     +--------------------------+
                     |      Pipeline Run        |
                     +--------------------------+
```

---

## Component Responsibilities

### Pipeline Registry

Responsible for:

* pipeline identity
* component references
* ownership metadata
* lifecycle management

Not responsible for:

* execution logic
* validation
* scheduling

---

### Schema Contract

Responsible for:

* parameter definitions
* validation rules
* required fields
* default values

Not responsible for:

* transformation logic
* orchestration

---

### Pipeline Template

Responsible for:

* execution flow
* processing logic
* reusable patterns
* transformation structure

Not responsible for:

* runtime values
* schedules

---

### Orchestration Definition

Responsible for:

* schedules
* dependencies
* triggers
* retries

Not responsible for:

* business logic
* validation

---

### Parameter Values

Responsible for:

* runtime configuration
* environment settings
* source definitions
* target definitions

Not responsible for:

* execution logic
* validation rules

---

## Dependency Comparison

### Legacy Model

```text
Pipeline
    |
    +--> Metadata Table
            |
            +--> Everything
```

### Reference-Based Model

```text
Pipeline
    |
    +--> Registry
            |
            +--> Schema Contract
            |
            +--> Template
            |
            +--> Orchestration
            |
            +--> Parameters
```

---

## Side-by-Side Comparison

| Category               | Legacy Architecture      | Reference Architecture |
| ---------------------- | ------------------------ | ---------------------- |
| Pipeline Identity      | Mixed with configuration | Registry               |
| Validation             | Embedded in metadata     | Schema Contract        |
| Execution Logic        | Embedded in metadata     | Template               |
| Scheduling             | Embedded in metadata     | Orchestration          |
| Runtime Values         | Mixed with logic         | Parameter Values       |
| Reuse                  | Limited                  | High                   |
| Coupling               | High                     | Low                    |
| Cohesion               | Low                      | High                   |
| Governance             | Difficult                | Easier                 |
| Regression Risk        | Higher                   | Lower                  |
| Extensibility          | Limited                  | High                   |
| Testing                | Difficult                | Easier                 |
| Operational Visibility | Lower                    | Higher                 |

---

## Architectural Principles

### Loose Coupling

Components communicate through references rather than direct dependencies.

### High Cohesion

Each component has a single well-defined responsibility.

### Open/Closed Principle

New pipeline patterns can be introduced without modifying existing components.

### Separation of Concerns

Validation, execution, orchestration, and configuration remain independent.

### Controlled Change Scope

Changes remain localized to the affected component.

---

## Operational Benefits

### Faster Development

New pipelines can be assembled from reusable components.

### Easier Governance

Ownership boundaries become clear.

### Safer Deployments

Reduced risk of platform-wide regressions.

### Improved Testing

Components can be validated independently.

### Better Platform Scalability

The framework can support larger numbers of pipelines without increasing complexity.

---

## Key Takeaway

The Reference-Based Pipeline Architecture transforms a monolithic metadata-driven framework into a composable architecture built around explicit references and independently managed components.

Rather than storing execution logic, validation rules, schedules, and runtime configuration in a single structure, responsibilities are separated into specialized components that can evolve independently.

The result is a platform that is easier to govern, safer to change, more reusable, and better suited for long-term enterprise-scale growth.
