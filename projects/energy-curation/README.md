# Energy Curation Framework

## Overview

This project demonstrates the design of a large-scale energy data curation framework that transforms raw operational, market, asset, ownership, and classification data into analytics-ready datasets.

The framework consolidates multiple source domains into a standardized curated model that supports reporting, forecasting, operational analytics, regulatory analysis, and business intelligence.

All table names, field names, and source-system references in this project are anonymized and generalized for public portfolio use.

---

## Business Problem

Energy data is typically distributed across many operational and market systems.

Common challenges include:

* Multiple source systems
* Effective-dated relationships
* Ownership changes over time
* Asset classification changes
* Market classification changes
* Large historical datasets
* Complex business rules
* Reporting consistency requirements

Without a curated data layer, analysts often spend significant time reconciling data manually across multiple systems.

---

## Solution

The Energy Curation Framework creates a standardized business-ready data layer that combines:

* Energy production data
* Market schedule data
* Resource ownership data
* Asset definition data
* Fuel and technology classification data
* Market reference data

into a unified curated dataset optimized for analytics and downstream consumption.

---

## High-Level Architecture

```text
                 SOURCE SYSTEMS

      +-------------------------------+
      | Energy Measurement Data       |
      +-------------------------------+

      +-------------------------------+
      | Ownership & Position Data     |
      +-------------------------------+

      +-------------------------------+
      | Asset Definition Data         |
      +-------------------------------+

      +-------------------------------+
      | Classification Reference Data |
      +-------------------------------+

      +-------------------------------+
      | Market Reference Data         |
      +-------------------------------+
                    |
                    v

             STANDARDIZED LAYER

                    |
                    v

          ENERGY CURATION ENGINE

                    |
                    v

          CURATED ENERGY DATA MART

                    |
        +-----------+-----------+
        |                       |
        v                       v

     Reporting            Analytics
```

---

## Business Objectives

The framework supports:

* Consistent reporting
* Historical accuracy
* Ownership analysis
* Asset performance analysis
* Energy production analysis
* Market participation analysis
* Fuel and technology mix analysis
* Executive dashboards

---

## Data Domains

### Energy Measurements

Includes generalized energy values such as:

* Actual energy
* Scheduled energy
* Forecasted energy
* Market-submitted energy
* Operational output

---

### Ownership and Position Data

Includes:

* Participant ownership
* Ownership percentages
* Effective date ranges
* Historical position changes

---

### Asset Definitions

Includes:

* Resource attributes
* Asset classifications
* Operational characteristics
* Capacity classifications
* Technology indicators

---

### Classification Data

Includes:

* Primary classification
* Secondary classification
* Technology category
* Reporting category

---

### Market Reference Data

Includes:

* Market identifiers
* Reporting dimensions
* Business grouping attributes
* Market participation attributes

---

## Curation Process

```text
Load Energy Measurement Data
          |
          v

Load Ownership Data
          |
          v

Load Asset Definition Data
          |
          v

Load Classification Data
          |
          v

Load Market Reference Data
          |
          v

Apply Effective-Dated Logic
          |
          v

Apply Business Rules
          |
          v

Generate Curated Dataset
```

---

## Effective-Dated Processing

Many enterprise energy datasets rely on effective-dated history.

The framework preserves point-in-time accuracy by selecting records where:

```sql
effective_start_date <= business_date
and effective_end_date > business_date
```

This ensures historical reports reflect the ownership, classification, and asset attributes that were valid at the time.

---

## Example Business Relationships

```text
Energy Measurement
      |
      +---- Ownership Attributes
      |
      +---- Asset Attributes
      |
      +---- Classification Attributes
      |
      +---- Market Reference Attributes
      |
      v

Curated Energy Record
```

---

## Core Business Rules

### Ownership Allocation

Energy values can be adjusted by ownership percentage.

Example:

```text
Measured Energy = 100 MW

Ownership Percentage = 50%

Allocated Energy = 50 MW
```

---

### Classification Assignment

Assets are grouped into generalized categories such as:

```text
Thermal

Renewable

Hydro

Nuclear

Storage

Other
```

---

### Asset Grouping

Assets may receive additional business classifications to support operational reporting, planning, and analytics.

---

## Curated Data Model

Example anonymized output fields:

```text
business_date

asset_identifier

asset_name

participant_identifier

participant_name

ownership_percentage

actual_energy_value

scheduled_energy_value

primary_classification

secondary_classification

market_category

asset_category

reporting_region

load_timestamp
```

---

## Example Join Architecture

```text
Energy Measurement Data
      |
      +---- Ownership Reference
      |
      +---- Asset Definition Reference
      |
      +---- Classification Reference
      |
      +---- Market Reference
      |
      v

Curated Energy Dataset
```

---

## Analytics Use Cases

### Energy Mix Reporting

Analyze production by:

* Classification
* Region
* Asset type
* Time period

---

### Ownership Analysis

Analyze:

* Participant share
* Ownership changes
* Portfolio exposure
* Historical ownership trends

---

### Market Performance

Compare:

* Scheduled values
* Actual values
* Forecasted values
* Variances

---

### Capacity and Planning Analytics

Support:

* Forecasting
* Resource adequacy
* Portfolio planning
* Strategic decision making

---

## Data Quality Controls

The framework validates:

### Ownership Reconciliation

Ownership percentages should reconcile within expected thresholds.

### Classification Completeness

All assets should map to valid classifications.

### Effective-Date Validity

Date ranges must be logically valid and non-conflicting.

### Reference Integrity

All required reference mappings should exist.

### Duplicate Detection

Business keys should remain unique at the curated grain.

---

## Performance Optimization

Techniques include:

### Partition Pruning

Reduce the amount of scanned data.

### Broadcast Joins

Optimize smaller reference table joins.

### Incremental Processing

Process only new or changed data.

### Delta Optimization

Improve query and storage performance.

### Historical Windowing

Process large historical ranges in controlled batches.

---

## Historical Preservation

The curated model preserves:

* Historical ownership changes
* Historical classification changes
* Historical asset attribute changes
* Historical market reference changes

This enables accurate point-in-time reporting.

---

## Example Reporting Outputs

### Energy by Classification

```text
Thermal       45%

Nuclear       25%

Hydro         12%

Renewable     15%

Other          3%
```

---

### Ownership Distribution

```text
Participant A   30%

Participant B   25%

Participant C   20%

Other           25%
```

---

## Technology Stack

Typical implementation:

* Azure Databricks
* Delta Lake
* Spark SQL
* PySpark
* Unity Catalog
* Azure Data Factory
* Cloud object storage
* Enterprise reporting tools

---

## Operational Benefits

### Consistent Reporting

Creates a common source of truth for energy analytics.

### Historical Accuracy

Supports point-in-time reporting.

### Better Governance

Centralizes business rules and reference logic.

### Improved Performance

Curated datasets are optimized for consumption.

### Faster Analytics

Reduces manual reconciliation effort.

---

## Lessons Learned

Key lessons from large-scale energy curation projects:

* Effective-dated joins are critical.
* Ownership history must be preserved.
* Classification mappings change over time.
* Business rules should be centralized.
* Curated models simplify downstream analytics.
* Governance and lineage are essential for trusted reporting.

---

## Future Enhancements

Potential future improvements include:

* Near real-time curation
* Forecast integration
* Predictive analytics
* AI-assisted anomaly detection
* Automated business rule generation
* Enhanced observability
* Self-service data product onboarding

---

## Key Takeaway

The Energy Curation Framework transforms fragmented operational and market energy data into a trusted, business-ready data product that supports reporting, analytics, forecasting, compliance, and strategic decision-making across the enterprise.
