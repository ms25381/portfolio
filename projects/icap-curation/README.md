# Capacity Curation Framework

## Overview

This project demonstrates a large-scale capacity curation framework designed to transform effective-dated market, resource, ownership, and asset attribute data into a trusted historical dataset.

The framework supports point-in-time reporting, regulatory analysis, portfolio analysis, operational planning, and enterprise analytics.

All table names, field names, source-system references, and organization-specific terms have been anonymized and generalized for public portfolio use.

---

## Business Problem

Capacity-related energy data is inherently time-dependent.

Resource ownership, asset classifications, reporting zones, capacity values, and operational characteristics can change over time.

Traditional ETL approaches often overwrite historical values, making it difficult to answer questions such as:

* Which participant owned a resource on a specific date?
* What was the capacity position for a participant during a historical period?
* Which reporting region was a resource assigned to at that point in time?
* How did ownership percentages change over time?
* What was the historical capacity exposure by participant, resource, region, or classification?

Accurate answers require point-in-time reconstruction using effective-dated source data.

---

## Solution

The Capacity Curation Framework creates daily historical capacity snapshots using effective-dated logic.

The framework evaluates ownership records, resource records, classification records, and reference records against a business date and selects only records valid for that date.

```sql
effective_start_date <= business_date
and effective_end_date > business_date
```

This allows the platform to reconstruct historical states accurately without exposing source-specific field names or source-system implementation details.

---

## High-Level Architecture

```text
                SOURCE SYSTEMS

       +-----------------------------+
       | Resource Ownership Data     |
       +-----------------------------+

       +-----------------------------+
       | Resource Attribute Data     |
       +-----------------------------+

       +-----------------------------+
       | Capacity Measurement Data   |
       +-----------------------------+

       +-----------------------------+
       | Classification Reference    |
       +-----------------------------+

       +-----------------------------+
       | Market Reference Data       |
       +-----------------------------+

                    |
                    v

          CAPACITY CURATION ENGINE

                    |
      +-------------+-------------+
      |                           |
      v                           v

 Daily Snapshot Logic     Historical Backfill Logic

                    |
                    v

        CURATED CAPACITY DATASET

                    |
                    v

      Reporting / Analytics / BI
```

---

## Key Features

### Point-in-Time Reconstruction

Supports historical analysis using effective-dated source records.

### Daily Snapshot Generation

Generates accurate daily capacity positions.

### Historical Backfill Support

Processes multiple years of historical data.

### Large-Scale Processing

Designed for high-volume distributed processing.

### Auditability

Preserves source timing context and load metadata.

### Incremental Processing

Supports efficient daily refreshes.

---

## Core Processing Flow

```text
Select Business Date
          |
          v

Load Ownership Records
          |
          v

Load Resource Attribute Records
          |
          v

Load Capacity Measurement Records
          |
          v

Load Reference Data
          |
          v

Apply Effective-Dated Logic
          |
          v

Join Ownership + Resource + Reference Data
          |
          v

Calculate Capacity Position
          |
          v

Generate Curated Output
          |
          v

Validation & Reconciliation
```

---

## Effective-Dated Data Model

Source systems typically maintain records using effective-dated history.

Anonymized example fields:

```text
effective_start_date

effective_end_date

resource_identifier

participant_identifier

capacity_value

ownership_percentage

source_load_timestamp
```

The curation engine evaluates each record against a target business date.

Example:

```text
Record A

Effective Start Date: 2024-01-01
Effective End Date:   2024-06-01

Valid Between:

2024-01-01 <= business_date < 2024-06-01
```

---

## Historical Processing Strategy

The framework supports several processing modes.

### Daily Loads

Used for production operations and routine refreshes.

### Monthly Backfills

Used for controlled historical rebuilds.

### Multi-Year Historical Loads

Used for:

* Initial deployment
* Data correction
* Audit requests
* Historical studies
* Large-scale validation

---

## Example Curated Data Model

Example anonymized output fields:

```text
business_date

participant_identifier

participant_name

resource_identifier

resource_name

reporting_region

primary_classification

secondary_classification

resource_category

capacity_value

allocated_capacity_value

ownership_percentage

effective_start_date

effective_end_date

record_created_timestamp

record_modified_timestamp
```

---

## Example Business Relationships

```text
Capacity Record
      |
      +---- Ownership Attributes
      |
      +---- Resource Attributes
      |
      +---- Classification Attributes
      |
      +---- Regional Reference Attributes
      |
      v

Curated Capacity Record
```

---

## Example Join Architecture

```text
Capacity Measurement Data
      |
      +---- Ownership Reference
      |
      +---- Resource Attribute Reference
      |
      +---- Classification Reference
      |
      +---- Market / Region Reference
      |
      v

Curated Capacity Dataset
```

---

## Business Rule Examples

### Ownership Allocation

Capacity values can be allocated by ownership percentage.

```text
Capacity Value = 100 MW

Ownership Percentage = 50%

Allocated Capacity Value = 50 MW
```

---

### Point-in-Time Attribute Selection

Resource attributes are selected based on the business date.

```text
Use the resource classification valid on the reporting date.
```

---

### Regional Assignment

Resources are mapped to reporting regions using the valid reference relationship for the business date.

```text
Resource + Business Date -> Reporting Region
```

---

## Performance Optimization

Several optimization techniques are commonly used.

### Historical Windowing

Large historical periods are processed in smaller windows.

### Monthly Processing Windows

Historical loads can be broken into monthly or multi-month batches.

### Predicate Pushdown

Filters are applied as early as possible.

### Partition Pruning

Curated data can be partitioned by reporting period.

### Parallel Processing

Independent historical windows can be processed concurrently.

### Incremental Logic

Daily production runs avoid unnecessary full reloads.

---

## Validation Framework

The pipeline includes multiple validation layers.

### Row Count Validation

Ensures expected record volumes.

### Duplicate Detection

Validates uniqueness of business keys.

### Null Analysis

Identifies missing critical business attributes.

### Historical Reconciliation

Compares curated outputs against source totals or prior baselines.

### Ownership Verification

Confirms ownership percentages and allocated values reconcile within expected thresholds.

---

## Example Validation Query

```sql
select
    business_date,
    participant_identifier,
    resource_identifier,
    count(*) as record_count
from curated_capacity_dataset
group by
    business_date,
    participant_identifier,
    resource_identifier
having count(*) > 1;
```

---

## Data Quality Controls

The framework checks for:

* Missing resource identifiers
* Missing participant identifiers
* Invalid effective-date ranges
* Overlapping effective-dated records
* Missing resource attributes
* Missing regional mappings
* Negative or unexpected capacity values
* Duplicate business keys

---

## Operational Considerations

### Runtime

Historical backfills can process multiple years of daily data.

### Memory

Effective-dated joins require careful distributed processing design.

### Partitioning

Output partitioning improves query and validation performance.

### Restartability

Windowed processing allows failed ranges to be rerun safely.

### Auditability

Preserving effective dates and load metadata improves troubleshooting.

---

## Business Benefits

### Improved Reporting Accuracy

Historical reports reflect the correct point-in-time business state.

### Faster Analytics

Analysts use curated datasets instead of manually reconstructing history.

### Regulatory Support

The framework supports audit and compliance reporting.

### Reduced Operational Risk

Centralized business logic reduces inconsistent reporting.

### Better Planning

Historical capacity trends support forecasting, resource planning, and strategic analysis.

---

## Example Use Cases

### Capacity Market Reporting

Historical capacity positions by participant, resource, region, and classification.

### Ownership Analysis

Track ownership changes over time.

### Resource Portfolio Analysis

Analyze capacity exposure by participant, asset category, and reporting region.

### Regulatory Audits

Reconstruct historical capacity positions for prior business dates.

### Executive Reporting

Provide trusted capacity metrics to stakeholders.

---

## Technology Stack

Typical implementation:

* Azure Databricks
* Spark SQL
* PySpark
* Delta Lake
* Unity Catalog
* Cloud object storage
* Workflow orchestration
* Git-based CI/CD
* Enterprise reporting tools

---

## Challenges Solved

### Historical Accuracy

Reconstructs exact historical states.

### Effective-Dated Complexity

Handles changing ownership, resource, and classification records.

### Large Data Volumes

Supports multi-year historical processing.

### Audit Requirements

Provides traceability and reproducibility.

### Reporting Consistency

Creates a trusted source for capacity reporting.

---

## Lessons Learned

Key lessons from capacity curation design:

* Effective-dated joins require careful design.
* Historical reconstruction should be deterministic and reproducible.
* Daily and historical processing logic should remain consistent.
* Validation is critical when processing time-based business data.
* Preserving source timing context improves auditability.
* Windowed processing improves performance and restartability.

---

## Future Enhancements

Potential future improvements include:

* Automated anomaly detection
* AI-assisted reconciliation
* Near real-time capacity monitoring
* Data lineage visualization
* Self-service historical replay
* Automated root cause analysis
* Predictive planning models

---

## Key Takeaway

The Capacity Curation Framework transforms complex effective-dated ownership, resource, classification, and capacity data into a trusted historical dataset that supports reporting, compliance, analytics, forecasting, and operational decision-making across large-scale energy market environments.
