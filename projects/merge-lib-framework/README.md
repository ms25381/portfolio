# Merge Library Framework

## Overview

This project demonstrates a reusable enterprise MERGE framework for Azure Databricks and Delta Lake.

The framework standardizes how data is inserted, updated, deleted, and synchronized across Bronze, Silver, and Gold layers while eliminating repetitive MERGE logic from individual pipelines.

Instead of each team writing custom Delta MERGE statements, developers define business rules through metadata and configuration, allowing the framework to generate and execute optimized MERGE operations automatically.

---

## Business Problem

Enterprise data platforms often contain hundreds of pipelines.

Each pipeline requires:

- Insert logic
- Update logic
- Delete logic
- Slowly Changing Dimension (SCD) handling
- Audit column management
- Duplicate prevention
- Data quality validation

Typical challenges include:

- Repeated MERGE code
- Inconsistent implementation
- High maintenance costs
- Complex onboarding
- Increased defect rates
- Difficult production support

As the number of pipelines grows, maintaining custom MERGE logic becomes increasingly expensive.

---

## Solution

The Merge Library Framework centralizes MERGE processing into a reusable component.

Pipeline developers provide:

- Source table
- Target table
- Business keys
- Update columns
- Audit fields
- SCD rules

The framework generates standardized Delta MERGE statements automatically.

---

## Architecture

```text
                SOURCE DATA

          Raw / Enriched Dataset

                      |
                      v

             MERGE LIBRARY

      +--------------------------+
      | Metadata Configuration   |
      +--------------------------+

      +--------------------------+
      | Validation Engine        |
      +--------------------------+

      +--------------------------+
      | Merge Generator          |
      +--------------------------+

      +--------------------------+
      | Audit Framework          |
      +--------------------------+

                      |
                      v

              Delta Lake MERGE

                      |
                      v

              Curated Dataset
```

---

## Key Features

### Reusable Framework

Single merge engine supports hundreds of pipelines.

### Metadata Driven

Configuration controls behavior.

### Delta Lake Integration

Leverages Delta MERGE operations.

### Audit Support

Automatically populates audit fields.

### SCD Support

Supports Slowly Changing Dimensions.

### Error Handling

Provides consistent exception management.

### Validation Framework

Pre-merge and post-merge validation.

---

## Core Processing Flow

```text
Load Source Data
         |
         v

Validate Input Data
         |
         v

Read Merge Configuration
         |
         v

Generate Merge Logic
         |
         v

Execute Delta MERGE
         |
         v

Capture Audit Metrics
         |
         v

Validation & Reconciliation
```

---

## Framework Components

### Merge Engine

Responsible for generating and executing merge operations.

### Metadata Layer

Stores merge definitions.

### Validation Layer

Performs pre-merge checks.

### Audit Layer

Captures operational metrics.

### Logging Layer

Records execution details.

---

## Supported Merge Types

### Insert Only

```text
New records inserted.

Existing records ignored.
```

### Upsert

```text
Insert new records.

Update existing records.
```

### Full Synchronization

```text
Insert

Update

Delete
```

### SCD Type 1

```text
Overwrite previous values.
```

### SCD Type 2

```text
Maintain historical versions.
```

---

## Example Configuration

```yaml
source_table:
  settlements.msrs_enriched.lmp_data

target_table:
  settlements.msrs_curated.lmp_curated

business_keys:
  - pnodeid
  - hour_utc

merge_type:
  upsert

audit_enabled:
  true
```

---

## Example Merge Logic

```sql
merge into target t
using source s
on t.id = s.id

when matched then
update set *

when not matched then
insert *
```

The framework generates this logic dynamically based on configuration.

---

## Audit Framework

The framework automatically captures:

```text
Pipeline Name

Run ID

Start Time

End Time

Duration

Records Read

Records Inserted

Records Updated

Records Deleted

Status

Error Details
```

---

## Example Audit Output

```text
Run ID: 12345

Records Read: 10,000

Inserted: 500

Updated: 2,100

Deleted: 0

Status: SUCCESS
```

---

## Data Quality Validation

### Duplicate Detection

Ensures business key uniqueness.

### Null Validation

Verifies required fields.

### Schema Validation

Checks column compatibility.

### Referential Integrity

Validates lookup relationships.

### Row Count Validation

Detects unexpected volume changes.

---

## Performance Optimization

### Partition Pruning

Limits data scanned.

### Predicate Pushdown

Reduces processing overhead.

### Delta Optimization

Improves storage efficiency.

### Parallel Processing

Supports large-scale workloads.

### Incremental Loads

Processes only changed data.

---

## Example Use Cases

### Raw to Enriched

Standardize source ingestion.

### Enriched to Curated

Apply business transformations.

### Reference Data Synchronization

Maintain lookup tables.

### Slowly Changing Dimensions

Track historical changes.

### Enterprise Data Warehouse Loading

Maintain analytical datasets.

---

## Technology Stack

- Azure Databricks
- Apache Spark
- PySpark
- Spark SQL
- Delta Lake
- Unity Catalog
- Azure Data Lake Storage Gen2
- Azure Data Factory
- GitLab CI/CD

---

## Benefits

### Reduced Development Time

Developers configure instead of coding.

### Improved Consistency

Standardized merge implementation.

### Easier Maintenance

Single framework manages merge behavior.

### Better Data Quality

Centralized validation rules.

### Lower Operational Risk

Consistent production behavior.

---

## Example Metrics

```text
Merge Success Rate

Average Runtime

Rows Processed

Rows Updated

Rows Inserted

Rows Deleted

Data Quality Failures

Pipeline Availability
```

---

## Lessons Learned

Key lessons from implementation:

- Metadata-driven merges scale significantly better than custom SQL.
- Centralized validation reduces production incidents.
- Standardized audit logging simplifies support.
- Explicit column mappings are more reliable than select * operations.
- Reusable frameworks dramatically improve onboarding speed.

---

## Future Enhancements

Potential future enhancements include:

- Automatic schema evolution
- AI-assisted merge optimization
- Dynamic partition tuning
- Data lineage integration
- Self-service pipeline onboarding
- Real-time merge monitoring

---

## Key Takeaway

The Merge Library Framework transforms repetitive Delta Lake merge development into a reusable, metadata-driven platform that improves consistency, scalability, maintainability, and operational reliability across enterprise data engineering environments.
