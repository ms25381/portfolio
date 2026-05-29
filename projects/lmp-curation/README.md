# Market Pricing Curation Framework

## Overview

This project demonstrates a large-scale market pricing curation framework implemented using a cloud lakehouse architecture.

The solution consolidates forward-looking market price data and real-time market price data into a trusted analytical dataset used for market analysis, settlement validation, price component analysis, congestion studies, transmission planning, operational monitoring, and executive reporting.

The framework is designed to process very large time-series datasets while maintaining historical accuracy, auditability, and high-performance query access.

All table names, field names, source-system names, and organization-specific identifiers have been anonymized and generalized for public portfolio use.

---

## Business Problem

Electricity markets generate high-volume pricing data at frequent intervals.

Each pricing location can contain multiple price components, such as:

* Total market price
* Congestion component
* Loss component
* Adjustment component
* Rate component
* Settlement-related component

Common challenges include:

* Multiple pricing source systems
* Very large historical datasets
* Historical corrections
* Missing reference mappings
* Duplicate records
* Time zone complexity
* Market settlement reconciliation
* High-performance analytical requirements

Without a curated solution, analysts spend significant time reconstructing pricing history and reconciling data across source systems.

---

## Solution

The Market Pricing Curation Framework provides:

* Historical market pricing repository
* Forward market and real-time market integration
* Pricing location enrichment
* Regional mapping enrichment
* Price component standardization
* Data quality validation
* High-performance analytical access

The curated dataset becomes a trusted source for downstream reporting, market analytics, settlement validation, and strategic decision-making.

---

## High-Level Architecture

```text
             MARKET SOURCE SYSTEMS

       +----------------------------+
       | Forward Market Pricing     |
       +----------------------------+

       +----------------------------+
       | Real-Time Market Pricing   |
       +----------------------------+

       +----------------------------+
       | Pricing Location Reference |
       +----------------------------+

       +----------------------------+
       | Regional Reference Data    |
       +----------------------------+

                    |
                    v

        MARKET PRICING CURATION ENGINE

                    |
        +-----------+-----------+
        |                       |
        v                       v

 Forward Market Logic    Real-Time Market Logic

                    |
                    v

          Reference Data Enrichment

                    |
                    v

       Curated Market Pricing Dataset

                    |
                    v

       Reporting / Analytics / BI
```

---

## Key Features

### Forward and Real-Time Price Consolidation

Combines forecasted, scheduled, or forward-looking market prices with real-time observed market prices.

### Historical Retention

Maintains complete historical pricing records for audit, trend analysis, and market studies.

### Pricing Location Enrichment

Adds business-friendly metadata for pricing points, nodes, hubs, interfaces, or other market locations.

### Regional Mapping

Associates pricing locations with reporting regions, zones, or business-defined groupings.

### Data Quality Validation

Detects duplicates, missing reference mappings, missing price components, and invalid records.

### High Performance

Optimized for large-scale analytical workloads and time-series queries.

---

## Source Domains

### Market Pricing Data

Generalized pricing inputs include:

```text
Forward market price data

Real-time market price data

Corrected market price data

Historical pricing data
```

---

### Reference Data

Generalized reference inputs include:

```text
Pricing location reference

Location-to-region relationship reference

Region definition reference

Market dimension reference
```

---

### Business Metadata

Generalized business metadata includes:

```text
Market attributes

Pricing location attributes

Regional attributes

Reporting categories
```

---

## Core Data Flow

```text
Load Forward Market Pricing
        |
        v

Load Real-Time Market Pricing
        |
        v

Load Pricing Location Reference
        |
        v

Load Regional Relationship Reference
        |
        v

Apply Business Rules
        |
        v

Enrich Pricing Data
        |
        v

Generate Curated Pricing Dataset
        |
        v

Validation & Reconciliation
```

---

## Example Curated Data Model

Example anonymized output fields:

```text
pricing_timestamp_utc

pricing_timestamp_local

pricing_location_identifier

pricing_location_name

pricing_location_type

reporting_region_name

total_price_value

congestion_price_component

loss_price_component

adjustment_price_component

rate_component

market_type_indicator

source_created_timestamp

source_modified_timestamp

load_timestamp

partition_period_key
```

---

## Time Zone Handling

The platform supports both technical and business reporting time zones.

### UTC Storage

Source timestamps are standardized and retained in UTC for consistency and auditability.

### Local Market Reporting Time

Business reporting can use a local market time zone representation.

### Daylight Saving Time Support

The framework handles daylight saving time transitions and local time ambiguity.

Example:

```text
UTC Timestamp

2025-01-01 05:00:00

Local Market Timestamp

2025-01-01 00:00:00
```

---

## Pricing Location Enrichment

Pricing records are enriched with business metadata.

Example:

```text
Pricing Location ID
        |
        v

Pricing Location Name
        |
        v

Pricing Location Type
        |
        v

Reporting Region
```

Supported generalized location categories may include:

```text
Hub

Aggregate

Interface

External Point

Real-Time Location

Residual / Settlement Location

Custom Reporting Location
```

---

## Regional Mapping

Regional enrichment uses generalized relationships such as:

```text
Pricing Location Reference
        |
        v

Location-to-Region Relationship
        |
        v

Region Definition Reference
```

This mapping allows analysts to aggregate pricing by reporting region, zone, market area, or other business-defined grouping.

---

## Data Quality Framework

The curation process performs automated validation.

### Duplicate Detection

Ensures uniqueness at the expected business grain.

### Null Analysis

Identifies missing values in:

* Reporting region
* Pricing location metadata
* Price components
* Market type indicator

### Historical Validation

Verifies completeness of historical loads.

### Referential Integrity

Validates that pricing records map to required reference data.

### Reconciliation

Compares source totals, record counts, and curated outputs against expected thresholds.

---

## Example Validation Query

```sql
select
    pricing_location_identifier,
    pricing_timestamp_local,
    market_type_indicator,
    count(*) as record_count
from curated_market_pricing_dataset
group by
    pricing_location_identifier,
    pricing_timestamp_local,
    market_type_indicator
having count(*) > 1;
```

---

## Performance Optimization

### Delta Lake Storage

Optimized storage layout for time-series analytics.

### Partitioning

A typical partitioning strategy uses a monthly or daily period key.

Example:

```text
202501

202502

202503
```

### Predicate Pushdown

Limits scanned data based on date, market type, location, and region filters.

### Incremental Processing

Processes only new, modified, or corrected records.

### Parallel Distributed Execution

Supports very large historical datasets.

### Optimization and Compaction

Improves query performance for downstream reporting tools.

---

## Example Analytical Use Cases

### Congestion Analysis

Identify regional congestion patterns and transmission bottlenecks.

### Market Monitoring

Track price volatility and market behavior.

### Settlement Validation

Validate settlement-related price components.

### Transmission Planning

Analyze regional pricing impacts over time.

### Executive Reporting

Provide high-level market performance metrics.

---

## Example KPIs

```text
Average Market Price

Peak Market Price

Congestion Component Cost

Loss Component Cost

Price Volatility

Regional Average Price

Hub Average Price

Forward vs Real-Time Spread
```

---

## Historical Preservation

The curated model preserves:

* Historical market prices
* Corrected pricing records
* Pricing location changes
* Regional mapping changes
* Source load and modification timestamps

This enables accurate point-in-time market reporting.

---

## Technology Stack

Typical implementation:

* Azure Databricks
* Apache Spark
* PySpark
* Spark SQL
* Delta Lake
* Unity Catalog
* Cloud object storage
* Workflow orchestration
* Git-based CI/CD
* Enterprise reporting tools

---

## Challenges Solved

### Massive Data Volumes

Supports very large historical pricing datasets.

### Historical Accuracy

Preserves historical and corrected market conditions.

### Complex Reference Data

Standardizes pricing location and regional mappings.

### Time Zone Complexity

Handles UTC and local business reporting time.

### High-Performance Analytics

Optimized for repeated time-series queries.

### Data Quality

Detects missing mappings, duplicates, and invalid price components.

---

## Business Benefits

### Trusted Pricing Repository

Creates a single source of truth for market price analytics.

### Faster Analytics

Eliminates repetitive data preparation and manual reconciliation.

### Improved Reporting

Standardizes pricing metrics across reporting teams.

### Better Decision Making

Supports market, operational, settlement, and planning analysis.

### Reduced Operational Risk

Automated validation improves reliability and downstream trust.

---

## Lessons Learned

Key lessons from large-scale market pricing curation:

* Reference data quality is critical.
* Time zone handling requires careful design.
* Historical market data grows rapidly.
* Partition strategy significantly impacts performance.
* Duplicate detection must be part of the core design.
* Automated validation prevents downstream reporting issues.
* Curated time-series models should preserve both technical and business timestamps.

---

## Future Enhancements

Potential future enhancements include:

* Real-time streaming price ingestion
* AI-assisted anomaly detection
* Automated root cause analysis
* Price forecasting models
* Market simulation integration
* Self-service analytics portal
* Data product publishing

---

## Key Takeaway

The Market Pricing Curation Framework transforms raw market pricing data into a trusted, high-performance analytical dataset that supports reporting, settlement validation, congestion analysis, market monitoring, forecasting, and strategic decision-making across large-scale energy market environments.
