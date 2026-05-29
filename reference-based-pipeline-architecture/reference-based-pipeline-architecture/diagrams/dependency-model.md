# Dependency Model

## Purpose

This diagram illustrates how dependencies are managed in the Reference-Based Pipeline Architecture.

Instead of embedding configuration, validation, execution logic, and scheduling directly inside pipelines, the architecture resolves these components through explicit references.

This approach minimizes coupling and allows individual components to evolve independently.

---

## Dependency Architecture

```text
                           DEPENDENCY MODEL

+------------------------------------------------------------+
|                    PIPELINE REGISTRY                        |
|                                                            |
|  pipeline_id                                                |
|  schema_contract_id                                         |
|  template_id                                                |
|  orchestration_id                                           |
+------------------------------------------------------------+
                           |
          +----------------+----------------+
          |                |                |
          v                v                v

+----------------+ +----------------+ +----------------------+
| SCHEMA         | | TEMPLATE       | | ORCHESTRATION        |
| CONTRACT       | | DEFINITION     | | DEFINITION           |
+----------------+ +----------------+ +----------------------+

          ^                ^
          |                |
          |                |
          +--------+-------+
                   |
                   v

          +------------------------+
          | PARAMETER VALUES       |
          | Runtime Configuration  |
          +------------------------+

                   |
                   v

          +------------------------+
          | EXECUTION PLAN         |
          +------------------------+

                   |
                   v

          +------------------------+
          | PIPELINE EXECUTION     |
          +------------------------+
