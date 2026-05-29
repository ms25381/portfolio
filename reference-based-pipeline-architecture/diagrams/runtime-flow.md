# Runtime Execution Flow

## Overview

This diagram illustrates how a pipeline is assembled procedurally at runtime from independently managed components.

Unlike traditional metadata-driven systems where logic is embedded directly into metadata, the reference-based architecture resolves structure first, validates configuration, and then builds an execution plan.

---

## Runtime Flow

```text
                    PIPELINE ID
                         |
                         v

              +----------------------+
              | Pipeline Registry    |
              +----------+-----------+
                         |
                         |
          +--------------+--------------+
          |                             |
          v                             v

+------------------+         +------------------+
| Schema Contract  |         | Pipeline Template|
+--------+---------+         +--------+---------+
         |                            |
         +------------+---------------+
                      |
                      v

          +--------------------------+
          | Parameter Values         |
          | Runtime Configuration    |
          +-------------+------------+
                        |
                        v

          +--------------------------+
          | Validation Engine        |
          +-------------+------------+
                        |
                        v

          +--------------------------+
          | Execution Plan Builder   |
          +-------------+------------+
                        |
                        v

          +--------------------------+
          | Pipeline Runtime         |
          | Databricks / Spark       |
          +-------------+------------+
                        |
                        v

          +--------------------------+
          | Curated Output           |
          | Delta Tables             |
          +--------------------------+
```

---

## Procedural Logic

```python
pipeline_id = get_pipeline_id()

schema_contract = get_schema_contract(
    pipeline_id
)

pipeline_template = get_pipeline_template(
    pipeline_id
)

parameters = get_parameters(
    pipeline_id
)

validate(
    schema_contract,
    parameters
)

execution_plan = derive_execution_plan(
    pipeline_template,
    schema_contract,
    parameters
)

execute(execution_plan)
```

---

## Benefits

### Early Validation

Invalid configuration is detected before execution begins.

### Reusable Templates

Execution behavior is shared across multiple pipelines.

### Reduced Coupling

Structure and configuration are managed independently.

### Easier Maintenance

Changes are localized to individual components.

### Improved Governance

Pipeline behavior can be traced through explicit references.

---

## Comparison

Traditional Model:

```text
Metadata
    |
    +--> Validation
    +--> Logic
    +--> Scheduling
    +--> Configuration
```

Reference-Based Model:

```text
Pipeline Registry
        |
        +--> Schema Contract
        +--> Template
        +--> Parameters
        +--> Orchestration
```

The runtime engine assembles these components dynamically during execution.
