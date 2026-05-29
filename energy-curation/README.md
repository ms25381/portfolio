# Energy Curation

## Overview

This project demonstrates the design and implementation of a large-scale energy curation pipeline used to transform raw market and operational energy data into analytics-ready datasets for reporting, forecasting, settlement analysis, and business intelligence.

The solution consolidates multiple market, generation, ownership, and fuel classification sources into a unified curated model supporting enterprise analytics and regulatory reporting.

---

## Business Problem

Energy market data is distributed across numerous operational systems.

Challenges include:

- Multiple source systems
- Complex business rules
- Effective-dated relationships
- Ownership changes over time
- Fuel classification changes
- Large historical datasets
- Reporting consistency requirements

Without a curated model, analysts spend significant time manually reconciling data from multiple systems.

---

## Solution

The Energy Curation Framework creates a standardized business layer that combines:

- Energy production
- Market schedules
- Resource ownership
- Unit definitions
- Fuel classifications
- Market dimensions

into a single curated dataset optimized for downstream analytics.

---

## High-Level Architecture

```text
                 SOURCE SYSTEMS

      +-------------------------------+
      | Energy Production Data        |
      +-------------------------------+

      +-------------------------------+
      | Resource Ownership Data       |
      +-------------------------------+

      +-------------------------------+
      | Unit Definitions              |
      +-------------------------------+

      +-------------------------------+
      | Fuel Type Definitions         |
      +-------------------------------+

      +-------------------------------+
      | Market Reference Data         |
      +-------------------------------+
                    |
                    v

             ENRICHED LAYER

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

The platform provides:

- Consistent reporting
- Historical accuracy
- Fuel type analysis
- Ownership analysis
- Resource performance tracking
- Market participation analysis
- Executive dashboards

---

## Data Domains

### Energy Production

Contains:

- Real-time MW
- Day-ahead MW
- Scheduled energy
- Actual generation

---

### Resource Ownership

Contains:

- Organization ownership
- Ownership percentages
- Effective date ranges

---

### Unit Definitions

Contains:

- Unit characteristics
- Capacity classifications
- Combined cycle indicators

---

### Fuel Classifications

Contains:

- Primary fuel
- Secondary fuel
- Fuel category mappings

---

### Market Dimensions

Contains:

- Market identifiers
- Trading dimensions
- Reporting attributes

---

## Curation Process

```text
Load Energy Data
         |
         v

Load Ownership Data
         |
         v

Load Unit Definitions
         |
         v

Load Fuel Mappings
         |
         v

Apply Effective Dating
         |
         v

Apply Business Rules
         |
         v

Generate Curated Dataset
```

---

## Effective-Dated Processing

Many source systems use SCD Type 2 style history.

The framework preserves historical accuracy by selecting records where:

```sql
effectiveday <= business_date
and terminationday > business_date
```

This ensures historical reports reflect the business reality that existed at the time.

---

## Example Business Relationships

```text
Energy Record
      |
      +---- Ownership Information
      |
      +---- Unit Definition
      |
      +---- Fuel Type
      |
      +---- Market Dimension
```

---

## Core Business Rules

### Ownership Allocation

Energy values are adjusted based upon ownership percentage.

Example:

```text
Actual Generation = 100 MW

Ownership = 50%

Owned Generation = 50 MW
```

---

### Fuel Classification

Units are categorized into:

```text
Coal

Natural Gas

Nuclear

Hydro

Solar

Wind

Oil

Other
```

---

### Combined Cycle Handling

Combined-cycle units receive additional business classifications to support operational reporting.

---

## Curated Data Model

Example output fields:

```text
business_date

unit_id

unit_name

org_id

ownership_factor

real_time_mw

day_ahead_mw

fuel_type

sub_fuel_type

market_name

capacity_class
```

---

## Example Join Architecture

```text
Energy Data
      |
      +---- Ownership Table
      |
      +---- Unit Definition
      |
      +---- Fuel Definition
      |
      +---- Market Dimension
      |
      v

Curated Energy Dataset
```

---

## Analytics Use Cases

### Fuel Mix Reporting

Analyze generation by:

- Fuel type
- Region
- Time period

---

### Ownership Analysis

Analyze:

- Company generation share
- Ownership trends
- Resource portfolios

---

### Market Performance

Compare:

- Day-ahead schedules
- Real-time production
- Variances

---

### Capacity Planning

Support:

- Forecasting
- Resource adequacy
- Strategic planning

---

## Data Quality Controls

The framework validates:

### Ownership Totals

Ownership percentages must reconcile.

### Fuel Assignments

All units require valid fuel mappings.

### Effective Dates

Date ranges must be valid.

### Market References

Dimension mappings must exist.

### Duplicate Detection

Business keys must remain unique.

---

## Performance Optimization

Techniques include:

### Partition Pruning

Reduce data scanning.

### Broadcast Joins

Optimize reference joins.

### Incremental Processing

Process only changed data.

### Delta Optimization

Improve query performance.

---

## Historical Preservation

The curated model preserves:

- Historical ownership changes
- Fuel reclassifications
- Unit definition changes
- Market structure changes

This enables accurate point-in-time reporting.

---

## Example Reporting Outputs

### Generation by Fuel

```text
Natural Gas    45%

Nuclear        25%

Coal           15%

Hydro           8%

Solar           5%

Wind            2%
```

---

### Ownership Distribution

```text
Company A   30%

Company B   25%

Company C   20%

Others      25%
```

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

## Operational Benefits

### Consistent Reporting

Single source of truth.

### Historical Accuracy

Point-in-time analysis.

### Better Governance

Standardized business logic.

### Improved Performance

Curated datasets optimized for consumption.

### Faster Analytics

Reduced reconciliation effort.

---

## Lessons Learned

Key lessons from large-scale energy curation projects:

- Effective-dated joins are critical.
- Ownership history must be preserved.
- Fuel mappings change over time.
- Business rules should be centralized.
- Curated models dramatically simplify analytics.
- Governance and lineage are essential for regulatory reporting.

---

## Future Enhancements

Potential future improvements include:

- Real-time curation
- Forecast integration
- Predictive analytics
- AI-assisted anomaly detection
- Automated business rule generation
- Enhanced observability

---

## Key Takeaway

The Energy Curation Framework transforms fragmented operational and market energy data into a trusted, business-ready data product that supports reporting, analytics, forecasting, regulatory compliance, and strategic decision-making across the enterprise.
