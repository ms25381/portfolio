# LMP Curation

## Overview

This project demonstrates a large-scale Locational Marginal Price (LMP) curation platform implemented using Azure Databricks, Delta Lake, and Spark.

The solution consolidates Day-Ahead (DA) and Real-Time (RT) electricity market pricing data into a trusted analytical dataset used for energy market analysis, settlement validation, congestion studies, transmission planning, and executive reporting.

The platform processes billions of records while maintaining historical accuracy, auditability, and high-performance query capabilities.

---

## Business Problem

Electricity markets generate massive volumes of pricing data every hour.

Each pricing point (PNode) contains multiple price components:

- Total LMP
- Congestion Price
- Loss Price
- Residual Adjustments
- Congestion Rates
- Loss Rates

Challenges include:

- Multiple source systems
- Billions of records
- Historical corrections
- Missing reference data
- Duplicate records
- Time zone complexities
- Settlement reconciliation requirements

Without a curated solution, analysts spend significant effort reconstructing pricing history.

---

## Solution

The LMP Curation framework provides:

- Historical LMP repository
- Day-Ahead and Real-Time integration
- PNode enrichment
- Zone enrichment
- Price component standardization
- Data quality validation
- High-performance analytical access

The curated dataset becomes the trusted source for all downstream reporting and analytics.

---

## Architecture

```text
             MARKET SOURCE SYSTEMS

       +----------------------------+
       | Day Ahead LMP              |
       +----------------------------+

       +----------------------------+
       | Real Time LMP              |
       +----------------------------+

       +----------------------------+
       | PNode Definitions          |
       +----------------------------+

       +----------------------------+
       | Zone Reference Data        |
       +----------------------------+

                    |
                    v

             LMP CURATION ENGINE

                    |
        +-----------+-----------+
        |                       |
        v                       v

    DA Processing         RT Processing

                    |
                    v

          Reference Data Joins

                    |
                    v

         Curated LMP Dataset

                    |
                    v

       Reporting / Analytics / BI
```

---

## Key Features

### DA and RT Consolidation

Combines Day-Ahead and Real-Time market pricing.

### Historical Retention

Maintains complete historical pricing records.

### PNode Enrichment

Adds business-friendly metadata.

### Zone Mapping

Associates PNodes with transmission zones.

### Data Quality Validation

Detects missing and invalid data.

### High Performance

Supports large-scale analytical workloads.

---

## Source Systems

### Market Pricing Sources

```text
s_pnodelmp_da
s_pnodelmp_rt
```

### Reference Data

```text
s_pnode

s_pnodexmssnzonerel

s_xmssnzonedef
```

### Business Metadata

```text
Market Dimensions

PNode Attributes

Zone Definitions
```

---

## Core Data Flow

```text
Load DA Pricing
        |
        v

Load RT Pricing
        |
        v

Load PNode Definitions
        |
        v

Load Zone Relationships
        |
        v

Apply Business Rules
        |
        v

Enrich Pricing Data
        |
        v

Generate Curated Dataset
        |
        v

Validation & Reconciliation
```

---

## Example Curated Fields

```text
hour_utc

hour_ept

pnodeid

pnodename

pnodetype

pnode_zone_name

totallmp

congestionprice

lossprice

residadjcongprice

residadjlossprice

congrate

lossrate

dayahead_flag

createddate_utc

modifieddate_utc
```

---

## Time Zone Handling

The platform supports:

### UTC Storage

All source timestamps retained in UTC.

### EPT Reporting

Business reporting uses Eastern Prevailing Time (EPT).

### DST Support

Handles Daylight Savings Time transitions.

Example:

```text
UTC Timestamp

2025-01-01 05:00:00

EPT Timestamp

2025-01-01 00:00:00
```

---

## PNode Enrichment

The platform enriches pricing records with business metadata.

Example:

```text
PNode ID
     |
     v

PNode Name
     |
     v

PNode Type
     |
     v

Transmission Zone
```

Supported node types include:

```text
HUB

AGGREGATE

EHVAGG

INTERFACE

EXT

RT

RESIDUAL_METERED_ED
```

---

## Zone Mapping

Zone enrichment uses:

```text
s_pnode
     |
     v

s_pnodexmssnzonerel
     |
     v

s_xmssnzonedef
```

This mapping allows analysts to aggregate pricing by transmission zone.

---

## Data Quality Framework

The curation process performs automated validation.

### Duplicate Detection

Ensures uniqueness of key business records.

### Null Analysis

Identifies missing:

- Zone names
- PNode metadata
- Pricing components

### Historical Validation

Verifies completeness of historical loads.

### Referential Integrity

Validates reference data joins.

---

## Example Validation Query

```sql
select
    pnodeid,
    hour_ept,
    count(*) as record_count
from rt_and_da_lmp_daily
group by
    pnodeid,
    hour_ept
having count(*) > 1;
```

---

## Performance Optimization

### Delta Lake

Optimized storage and retrieval.

### Partitioning

Typical partition key:

```text
hour_month_partkey
```

Example:

```text
202501

202502

202503
```

### Predicate Pushdown

Limits data scanned.

### Incremental Processing

Processes only changed data.

### Parallel Spark Execution

Supports billions of records.

---

## Example Analytical Use Cases

### Congestion Analysis

Identify transmission bottlenecks.

### Market Monitoring

Track price volatility.

### Settlement Validation

Validate settlement calculations.

### Transmission Planning

Analyze regional pricing impacts.

### Executive Reporting

Provide market performance metrics.

---

## Example KPIs

```text
Average LMP

Peak LMP

Congestion Cost

Loss Cost

Price Volatility

Zone Average Price

Hub Average Price

DA vs RT Spread
```

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
- Tableau

---

## Challenges Solved

### Massive Data Volumes

Supports billions of pricing records.

### Historical Accuracy

Preserves historical market conditions.

### Complex Reference Data

Standardizes PNode and zone mappings.

### Performance

Provides sub-second analytical access.

### Data Quality

Detects and prevents data issues.

---

## Business Benefits

### Trusted Pricing Repository

Single source of truth for market prices.

### Faster Analytics

Eliminates repetitive data preparation.

### Improved Reporting

Consistent metrics across departments.

### Better Decision Making

Supports market and operational analysis.

### Reduced Operational Risk

Automated validation improves reliability.

---

## Lessons Learned

Key lessons from implementation:

- Reference data quality is critical.
- Time zone handling requires careful design.
- Historical market data grows rapidly.
- Partition strategy significantly impacts performance.
- Automated validation prevents downstream reporting issues.

---

## Future Enhancements

Potential enhancements include:

- Real-time streaming LMP ingestion
- AI-assisted anomaly detection
- Automated root cause analysis
- Price forecasting models
- Market simulation integration
- Self-service analytics portal

---

## Key Takeaway

The LMP Curation platform transforms raw electricity market pricing data into a trusted, high-performance analytical dataset that supports reporting, settlement validation, congestion analysis, market monitoring, and strategic decision-making across large-scale energy market environments.
