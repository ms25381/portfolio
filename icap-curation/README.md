# ICAP Curation

## Overview

This project demonstrates a large-scale Installed Capacity (ICAP) curation solution implemented using Azure Databricks, Delta Lake, and Spark.

The solution transforms effective-dated market and resource ownership data into a trusted, point-in-time historical dataset suitable for capacity market reporting, regulatory compliance, financial analysis, and operational planning.

The project was designed to solve one of the most common challenges in energy and utility analytics: reconstructing the exact state of ownership and installed capacity on any given business date.

---

## Business Problem

Energy market data is inherently time-dependent.

Resource ownership, fuel types, zonal assignments, capacity values, and operational characteristics frequently change over time.

Traditional ETL approaches often overwrite historical values, making it difficult to answer questions such as:

- Who owned a generating unit on a specific date?
- What was the installed capacity position of an organization last year?
- Which zone was a resource assigned to at that point in time?
- How did ownership percentages change historically?
- What was the historical ICAP exposure by company or market participant?

Accurate answers require point-in-time reconstruction using effective-dated source data.

---

## Solution

The ICAP Curation framework creates daily historical snapshots using effective-date logic.

The system evaluates both ownership records and resource attributes against a business date and only selects records valid for that date.

```sql
effectiveday <= business_date
and terminationday > business_date
```

This allows the platform to accurately reconstruct historical states without storing redundant daily snapshots in source systems.

---

## Architecture

```text
                SOURCE SYSTEMS

       +--------------------------+
       | Resource Ownership Data |
       +--------------------------+

       +--------------------------+
       | Resource Definition Data |
       +--------------------------+

       +--------------------------+
       | Market Reference Data    |
       +--------------------------+

                    |
                    v

          ICAP CURATION ENGINE

                    |
      +-------------+-------------+
      |                           |
      v                           v

 Daily Snapshot Logic     Historical Backfill Logic

                    |
                    v

           CURATED ICAP DATASET

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

### Large Scale Processing

Optimized for billions of records using Spark.

### Auditability

Preserves effective dates and source lineage.

### Incremental Processing

Supports efficient daily updates.

---

## Core Processing Flow

```text
Select Business Date
         |
         v

Load Ownership Records
         |
         v

Load Resource Definitions
         |
         v

Apply Effective-Date Logic
         |
         v

Join Ownership + Resource Data
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

Source systems typically maintain records with:

```text
effective_day

termination_day

resource_id

organization_id

owned_mw
```

The curation engine evaluates each record against a target business date.

Example:

```text
Record A

Effective Day:   2024-01-01
Termination Day: 2024-06-01

Valid Between:

2024-01-01 <= business_date < 2024-06-01
```

---

## Historical Processing Strategy

The framework supports:

### Daily Loads

Used for production operations.

### Monthly Backfill

Used for historical rebuilds.

### Multi-Year Historical Loads

Used for:

- Initial deployment
- Data correction
- Audit requests
- Capacity studies

---

## Example Curated Fields

```text
business_date

organization_id

organization_name

resource_id

resource_name

zone_name

fuel_type

resource_type

owned_mw

installed_capacity_mw

ownership_factor

effective_day

termination_day

created_timestamp

modified_timestamp
```

---

## Performance Optimization

Several optimization techniques were implemented:

### Monthly Processing Windows

Large historical periods are broken into smaller batches.

### Predicate Pushdown

Filters applied as early as possible.

### Delta Lake Optimization

Leverages partition pruning and optimized storage.

### Parallel Processing

Historical ranges processed concurrently.

### Incremental Logic

Avoids unnecessary full reloads.

---

## Validation Framework

The pipeline includes multiple validation layers.

### Row Count Validation

Ensures expected record volumes.

### Duplicate Detection

Validates uniqueness of business keys.

### Null Analysis

Identifies missing critical fields.

### Historical Reconciliation

Compares outputs against source systems.

### Ownership Verification

Confirms ownership percentages are accurate.

---

## Example Validation Query

```sql
select
    business_date,
    organization_id,
    resource_id,
    count(*) as record_count
from installed_capacity_daily
group by
    business_date,
    organization_id,
    resource_id
having count(*) > 1;
```

---

## Technology Stack

- Azure Databricks
- Spark SQL
- PySpark
- Delta Lake
- Unity Catalog
- Azure Data Lake Storage Gen2
- Azure Data Factory
- GitLab CI/CD
- Databricks Workflows

---

## Challenges Solved

### Historical Accuracy

Reconstructs exact historical states.

### Effective-Dated Complexity

Handles overlapping ownership and attribute records.

### Large Data Volumes

Supports multi-year historical processing.

### Audit Requirements

Provides traceable lineage and reproducibility.

### Reporting Consistency

Creates a single trusted source for capacity reporting.

---

## Business Benefits

### Improved Reporting Accuracy

Historical reports reflect actual point-in-time values.

### Faster Analytics

Analysts query curated datasets rather than reconstructing history.

### Regulatory Compliance

Supports audit and compliance requirements.

### Reduced Operational Risk

Centralized business logic reduces inconsistencies.

### Better Capacity Planning

Provides reliable historical capacity trends.

---

## Example Use Cases

### Capacity Market Reporting

Historical capacity positions by organization.

### Ownership Analysis

Track ownership changes over time.

### Resource Portfolio Management

Analyze capacity exposure by resource type.

### Regulatory Audits

Reconstruct historical market positions.

### Executive Reporting

Provide trusted capacity metrics to business stakeholders.

---

## Lessons Learned

Key lessons from the implementation:

- Effective-dated joins require careful design.
- Historical reconstruction should be deterministic and reproducible.
- Daily and historical processing logic should remain identical.
- Validation is critical when processing time-based business data.
- Performance optimization becomes increasingly important as historical windows grow.

---

## Future Enhancements

Potential future enhancements include:

- Automated anomaly detection
- AI-assisted reconciliation
- Real-time capacity monitoring
- Data lineage visualization
- Self-service historical replay
- Automated root cause analysis

---

## Key Takeaway

The ICAP Curation framework transforms complex effective-dated ownership and resource data into a trusted historical capacity dataset that supports reporting, compliance, analytics, and operational decision-making across large-scale energy market environments.
