# Enriched-to-Curated Framework

## Overview

This project demonstrates a reusable framework for transforming standardized enriched (Silver) datasets into business-ready curated (Gold) data products within a Delta Lakehouse architecture.

The framework provides a consistent pattern for applying business rules, dimensional enrichment, aggregations, calculations, and reporting optimizations while maintaining governance, lineage, and scalability.

---

## Business Problem

After raw data has been ingested and standardized in the Enriched layer, organizations still face challenges:

- Business rules scattered across pipelines
- Duplicate transformation logic
- Inconsistent reporting definitions
- Poor governance
- Difficult onboarding
- Slow development cycles
- Limited reuse across teams

Without a standardized curation framework, every project develops its own transformation patterns.

---

## Solution

The Enriched-to-Curated Framework provides a common architecture for:

- Business rule implementation
- Curated table generation
- Data quality validation
- Historical preservation
- Dimensional enrichment
- KPI calculation
- Reporting optimization

The framework enables teams to rapidly create trusted business datasets while maintaining consistency across the enterprise.

---

## High-Level Architecture

```text
               ENRICHED LAYER (Silver)

      +-----------------------------------+
      | Standardized Operational Data     |
      +-----------------------------------+

      +-----------------------------------+
      | Reference Data                    |
      +-----------------------------------+

      +-----------------------------------+
      | Master Data                       |
      +-----------------------------------+
                       |
                       v

          ENRICHED-TO-CURATED FRAMEWORK

                       |
       +---------------+---------------+
       |               |               |
       v               v               v

 Business Rules   Data Quality   Enrichment

                       |
                       v

              CURATED LAYER (Gold)

                       |
         +-------------+-------------+
         |                           |
         v                           v

      Reporting                Analytics
```

---

## Medallion Architecture Context

```text
RAW (Bronze)
      |
      v

ENRICHED (Silver)
      |
      v

CURATED (Gold)
```

### Raw Layer

Stores source-aligned data.

### Enriched Layer

Applies cleansing, standardization, and conformance.

### Curated Layer

Provides business-ready datasets.

---

## Framework Objectives

### Standardization

Common transformation patterns.

### Reusability

Shared pipeline architecture.

### Scalability

Support hundreds of curated datasets.

### Governance

Centralized business logic.

### Performance

Optimized reporting structures.

---

## Core Components

### Business Rule Engine

Applies domain-specific transformations.

### Enrichment Layer

Adds dimensions and reference data.

### Aggregation Engine

Computes business metrics.

### Validation Layer

Ensures output quality.

### Publishing Layer

Publishes curated tables.

---

## Typical Processing Flow

```text
Load Enriched Data
          |
          v

Validate Input
          |
          v

Apply Business Rules
          |
          v

Join Reference Data
          |
          v

Calculate Metrics
          |
          v

Validate Output
          |
          v

Publish Curated Table
```

---

## Common Curation Activities

### Business Calculations

Examples:

```text
Revenue

Margin

Ownership Factors

Capacity Values

Risk Scores
```

### Data Enrichment

Examples:

```text
Market Dimensions

Customer Dimensions

Product Dimensions

Geographic Dimensions
```

### KPI Generation

Examples:

```text
Daily Totals

Monthly Totals

Rolling Averages

Utilization Rates
```

---

## Example Curated Data Model

```text
Business Date

Customer ID

Product ID

Market ID

Revenue

Cost

Margin

Status

Load Timestamp
```

---

## Data Quality Integration

The framework performs:

### Completeness Checks

Required fields populated.

### Referential Integrity

Dimension relationships validated.

### Duplicate Detection

Business keys remain unique.

### Business Rule Validation

Calculated values verified.

### Reconciliation

Source versus target totals checked.

---

## Historical Data Handling

Supports:

### SCD Type 1

Current-state reporting.

### SCD Type 2

Historical preservation.

### Point-in-Time Reporting

Accurate historical analysis.

---

## Example Use Cases

### Energy Markets

- LMP curation
- Capacity curation
- Settlement reporting

### Financial Services

- Revenue reporting
- Risk aggregation
- Regulatory reporting

### Manufacturing

- Production metrics
- Yield calculations

### Healthcare

- Claims reporting
- Member analytics

---

## Business Rule Example

Input:

```text
Actual Generation = 100 MW

Ownership Factor = 0.75
```

Output:

```text
Owned Generation = 75 MW
```

---

## Dimensional Enrichment Example

```text
Transaction Data
        |
        +---- Customer Dimension
        |
        +---- Market Dimension
        |
        +---- Product Dimension
        |
        v

Curated Dataset
```

---

## Performance Optimization

Techniques include:

### Partitioning

Reduce scan volume.

### Incremental Processing

Process only changed data.

### Delta Optimization

Improve query performance.

### Broadcast Joins

Accelerate dimension lookups.

### Materialized Outputs

Support fast reporting.

---

## Governance Features

### Metadata Registration

All curated datasets documented.

### Data Lineage

Source-to-target traceability.

### Audit Logging

Operational transparency.

### Ownership Tracking

Clear accountability.

---

## Operational Benefits

### Faster Development

Reusable framework components.

### Better Consistency

Shared business logic.

### Improved Data Quality

Integrated validation.

### Easier Maintenance

Centralized architecture.

### Improved Governance

Standardized controls.

---

## Technology Stack

Typical implementation:

- Azure Databricks
- Delta Lake
- Spark SQL
- PySpark
- Delta Live Tables
- Unity Catalog
- Azure Data Factory

---

## Example Curated Outputs

### Energy Domain

```text
hourly_lmp_curated

installed_capacity_curated

energy_by_owner_curated
```

### Financial Domain

```text
daily_revenue_curated

monthly_profitability_curated
```

### Operational Domain

```text
asset_performance_curated

production_metrics_curated
```

---

## Lessons Learned

Key lessons from enterprise curation projects:

- Business rules should be centralized.
- Curated models must remain business-focused.
- Data quality should be integrated into every stage.
- Metadata significantly improves maintainability.
- Governance and lineage are critical for trust.
- Reusable frameworks reduce technical debt.

---

## Future Enhancements

Potential future capabilities:

- AI-assisted business rule generation
- Automated lineage capture
- Semantic layer integration
- Data product marketplace
- Automated KPI discovery
- Real-time curation pipelines

---

## Key Takeaway

The Enriched-to-Curated Framework provides a scalable and governed architecture for transforming standardized enterprise data into trusted business-ready datasets that support reporting, analytics, machine learning, and strategic decision-making across the organization.
