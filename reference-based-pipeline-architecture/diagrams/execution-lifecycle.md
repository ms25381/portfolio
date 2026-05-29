# Execution Lifecycle

## Purpose

This diagram illustrates the complete lifecycle of a pipeline execution within the Reference-Based Pipeline Architecture.

The architecture separates structure resolution, validation, orchestration, and execution into distinct stages to improve transparency, governance, troubleshooting, and operational reliability.

---

## High-Level Lifecycle

```text
                    EXECUTION LIFECYCLE

+--------------------------------------------------+
|                  Pipeline Request                |
+-------------------------+------------------------+
                          |
                          v

+--------------------------------------------------+
|              Resolve Pipeline Registry           |
+-------------------------+------------------------+
                          |
                          v

+--------------------------------------------------+
|             Resolve Schema Contract              |
+-------------------------+------------------------+
                          |
                          v

+--------------------------------------------------+
|             Resolve Pipeline Template            |
+-------------------------+------------------------+
                          |
                          v

+--------------------------------------------------+
|           Resolve Orchestration Definition       |
+-------------------------+------------------------+
                          |
                          v

+--------------------------------------------------+
|               Load Parameter Values              |
+-------------------------+------------------------+
                          |
                          v

+--------------------------------------------------+
|               Validate Parameters                |
+-------------------------+------------------------+
                          |
                    Valid ?
                   /       \
                 No         Yes
                 |           |
                 v           v

        +----------------+   +----------------------+
        | Validation     |   | Build Execution Plan |
        | Failure        |   +----------+-----------+
        +----------------+              |
                                        v

                          +--------------------------+
                          | Execute Pipeline Steps   |
                          +------------+-------------+
                                       |
                                       v

                          +--------------------------+
                          | Collect Runtime Metrics  |
                          +------------+-------------+
                                       |
                                       v

                          +--------------------------+
                          | Update Run Logs          |
                          +------------+-------------+
                                       |
                                       v

                          +--------------------------+
                          | Pipeline Completed       |
                          +--------------------------+
```

---

## Runtime Resolution Sequence

```text
1. Pipeline Selected

2. Registry Loaded

3. Component References Resolved

4. Schema Contract Loaded

5. Template Loaded

6. Orchestration Loaded

7. Runtime Parameters Loaded

8. Validation Performed

9. Execution Plan Generated

10. Pipeline Executed

11. Monitoring Metrics Captured

12. Run Logs Updated

13. Execution Completed
```

---

## Execution Example

```text
pipeline_id = customer_curated_daily

Registry
    |
    +--> schema_customer_v1
    |
    +--> curated_incremental_template
    |
    +--> daily_midnight_schedule

Schema Contract
    |
    +--> validates parameters

Template
    |
    +--> generates execution plan

Execution Engine
    |
    +--> executes pipeline steps

Monitoring
    |
    +--> records metrics and status
```

---

## Lifecycle Stages

### Stage 1: Discovery

Identify pipeline and load registry metadata.

Outputs:

* pipeline identity
* component references

---

### Stage 2: Resolution

Resolve all referenced components.

Outputs:

* schema contract
* template definition
* orchestration definition

---

### Stage 3: Validation

Validate runtime configuration against schema requirements.

Outputs:

* validation success
* validation failure

---

### Stage 4: Planning

Build executable runtime plan.

Outputs:

* ordered execution steps
* dependency graph
* runtime configuration

---

### Stage 5: Execution

Execute pipeline tasks.

Outputs:

* transformed data
* execution metrics
* status information

---

### Stage 6: Monitoring

Capture operational information.

Outputs:

* duration
* row counts
* errors
* warnings

---

### Stage 7: Completion

Update run history and publish final status.

Outputs:

* success
* failure
* audit trail

---

## Failure Points

Possible failures may occur during:

### Registry Resolution

* pipeline not found
* invalid component references

### Validation

* missing required parameters
* invalid parameter types

### Planning

* template resolution errors
* dependency resolution failures

### Execution

* source unavailable
* transformation failures
* infrastructure issues

### Monitoring

* logging failures
* metrics collection failures

---

## Operational Benefits

### Predictable Execution

Every pipeline follows the same lifecycle.

### Easier Troubleshooting

Failures can be isolated to specific lifecycle stages.

### Better Governance

Validation occurs before execution.

### Improved Monitoring

Operational metrics are consistently captured.

### Higher Reliability

Invalid configurations are rejected before processing begins.

---

## Architectural Principle

Execution should never begin until:

* pipeline identity is resolved
* component references are resolved
* parameters are validated
* execution plans are generated

This ensures that execution remains deterministic, auditable, and governed by explicit contracts rather than runtime assumptions.
