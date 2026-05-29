# Dependency Model

## Purpose

This diagram illustrates how pipeline components depend upon one another through explicit references.

The objective is to eliminate hidden dependencies, reduce coupling, improve maintainability, and provide a transparent dependency chain from pipeline registration through execution.

---

## High-Level Dependency Graph

```text
                              PIPELINE REGISTRY
                       (Central Pipeline Catalog)
                                       |
                                       |
             +-------------------------+-------------------------+
             |                         |                         |
             v                         v                         v

      SCHEMA CONTRACT         PIPELINE TEMPLATE         ORCHESTRATION
       (Validation)            (Execution Logic)       (Scheduling)

                                       |
                                       |
                                       v

                              PARAMETER VALUES
                            (Runtime Configuration)

                                       |
                                       |
                                       v

                                EXECUTION PLAN

                                       |
                                       |
                                       v

                                 PIPELINE RUN
```

---

## Component Dependency Hierarchy

```text
Pipeline Run
     |
     +--> Execution Plan
              |
              +--> Pipeline Template
              |
              +--> Schema Contract
              |
              +--> Parameter Values

Parameter Values
     |
     +--> Schema Contract

Pipeline Registry
     |
     +--> Schema Contract
     |
     +--> Pipeline Template
     |
     +--> Orchestration
```

---

## Dependency Resolution Sequence

During execution, dependencies are resolved in the following order:

```text
1. Locate Pipeline ID

2. Read Pipeline Registry

3. Resolve Schema Contract

4. Resolve Pipeline Template

5. Resolve Orchestration

6. Load Parameter Values

7. Validate Parameters

8. Build Execution Plan

9. Execute Pipeline
```

---

## Runtime Example

```text
Pipeline ID
    |
    v

customer_curated_pipeline

    |
    v

Pipeline Registry
    |
    +--> schema_contract_id = schema_customer_v2
    |
    +--> template_id = curated_load_template
    |
    +--> orchestration_id = daily_midnight_schedule

    |
    v

Schema Contract

    |
    v

Validate Parameters

    |
    v

Pipeline Template

    |
    v

Generate Execution Plan

    |
    v

Pipeline Execution
```

---

## Dependency Ownership

| Component         | Owned By                  |
| ----------------- | ------------------------- |
| Pipeline Registry | Platform Team             |
| Schema Contract   | Data Governance Team      |
| Pipeline Template | Platform Engineering Team |
| Orchestration     | Operations Team           |
| Parameter Values  | Pipeline Owner            |
| Execution Plan    | Runtime Engine            |

---

## Dependency Rules

### Rule 1

Pipeline Registry may reference:

* Schema Contracts
* Pipeline Templates
* Orchestration Definitions

### Rule 2

Schema Contracts must not reference:

* Templates
* Orchestration
* Runtime Parameters

### Rule 3

Templates must not contain:

* Hard-coded schedules
* Hard-coded pipeline identities
* Hard-coded business values

### Rule 4

Orchestration must not define:

* Business logic
* Validation logic
* Transformation logic

### Rule 5

Parameter Values must conform to Schema Contracts.

---

## Design Benefits

### Explicit Dependencies

All relationships are visible and discoverable.

### Reduced Coupling

Components evolve independently.

### Easier Troubleshooting

Dependency chains can be traced quickly.

### Better Governance

Ownership boundaries are clearly defined.

### Higher Reuse

Templates and schemas can be reused across many pipelines.

### Safer Change Management

Changes remain localized to individual components.

---

## Architectural Principle

The architecture intentionally favors:

* Explicit references over implicit assumptions
* Composition over inheritance
* Configuration over hard-coding
* Reusable components over duplicated implementations

The resulting system is easier to govern, easier to extend, and less likely to experience platform-wide regressions when new pipelines are introduced.

