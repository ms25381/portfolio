# Portfolio — John Shia

Senior AI Engineer | Data Engineer | Data Architect
Azure Databricks • Spark/PySpark • Delta Lake • Cloud Data Platforms • IoT • AI Engineering

---

## Overview

This portfolio contains architecture patterns, platform designs, reference implementations, migration frameworks, governance models, dashboard examples, and technical writeups based on enterprise-scale data and AI platform work.

The focus is on practical engineering patterns:

* Azure Databricks Lakehouse architecture
* Metadata-driven pipeline frameworks
* Data quality and observability
* Industrial IoT and time-series analytics
* Energy and utility data curation
* Cloud migration and platform modernization
* AI-ready data platform design

All examples use synthetic data, anonymized architectures, generalized naming conventions, and reusable implementation patterns.

No employer confidential information, proprietary source code, customer data, or internal documentation is included.

---

## Contact

* Email: [john.shia.ga@outlook.com](mailto:john.shia.ga@outlook.com)
* LinkedIn: https://www.linkedin.com/in/john-shia-33134320a/

---

## Start Here

### Core Portfolio Projects

| Area                     | Project                                                                                    | Description                                                                                                  |
| ------------------------ | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------------------------------------------------------ |
| Enterprise Data Platform | [Electric Grid Data Platform](./projects/electric-grid-data-platform/)                     | Enterprise-scale operational and analytical data platform for telemetry, operational systems, and reporting. |
| Lakehouse Curation       | [Energy Curation](./projects/energy-curation/)                                             | Curated energy analytics layer using anonymized tables, fields, and business rules.                          |
| Capacity Analytics       | [iCAP Curation](./projects/icap-curation/)                                                 | Historical and daily curation framework using effective-dated data and SCD-style processing.                 |
| Market Analytics         | [LMP Curation](./projects/lmp-curation/)                                                   | High-volume time-series curation pattern for pricing and market analytics.                                   |
| Observability            | [Databricks Monitoring Dashboard](./projects/databricks-monitoring-dashboard/)             | Databricks dashboard design for pipeline health, run history, and operational analytics.                     |
| Data Quality             | [DQ Metadata Framework](./projects/dq-metadata-framework/)                                 | Metadata-driven data quality rules, validation automation, and operational diagnostics.                      |
| Deployment               | [Azure Databricks Deployment Framework](./projects/azure-databricks-deployment-framework/) | Deployment framework for promoting Databricks assets across environments.                                    |
| Industrial IoT           | [Synthetic IoT Data Generator](./projects/synthetic-iot-data-generator/)                   | Synthetic industrial telemetry generator for demos, analytics, and AI-ready data pipelines.                  |

---

## Related Public Repositories

| Repository                                                              | Purpose                                                                                               |
| ----------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------- |
| [engineering-articles](https://github.com/ms25381/engineering-articles) | Technical articles, anonymized Confluence-style writeups, architecture notes, and thought leadership. |
| [presentations](https://github.com/ms25381/presentations)               | Technical presentations, architecture walkthroughs, interview prep materials, and learning decks.     |
| [synthetic-datasets](https://github.com/ms25381/synthetic-datasets)     | Synthetic datasets and sample generators for data engineering, AI, streaming, and IoT examples.       |
| [architecture-notes](https://github.com/ms25381/architecture-notes)     | Architecture decision records, design notes, migration strategies, and reference architectures.       |

---

# Areas of Expertise

## Data Engineering

* Azure Databricks
* Spark SQL
* PySpark
* Delta Lake
* Medallion Architecture
* Data Lakehouse Design
* CDC Pipelines
* SCD Type 2 Processing
* Metadata-Driven ETL
* Batch and streaming pipeline design

## AI Engineering

* Generative AI
* Retrieval Augmented Generation (RAG)
* Vector Databases
* AI Agents
* LangChain
* Bedrock
* OpenAI APIs
* MLOps
* AI Infrastructure
* AI-ready data platform design

## Cloud Platforms

### Azure

* Azure Databricks
* Azure Data Factory
* ADLS Gen2
* Synapse Analytics
* Azure SQL
* Unity Catalog
* Microsoft Purview patterns

### AWS

* S3
* Lambda
* Kinesis
* Glue
* Bedrock
* Athena
* MSK / streaming patterns

### GCP

* BigQuery
* Pub/Sub
* Dataflow
* Cloud Storage

## Industry Experience

* Electric Grid Operations
* Energy Markets
* Utilities
* Manufacturing
* Mining
* Healthcare
* Financial Services
* Enterprise Data Platforms

---

# Recommended Reading Order

## 1. Enterprise Data Platforms

### [electric-grid-data-platform](./projects/electric-grid-data-platform/)

Enterprise-scale operational and analytical data platform supporting telemetry, operational systems, and business reporting.

**Topics**

* Data Lakehouse
* Grid Operations
* Enterprise Analytics
* Operational Data Integration

---

### [scada-data-platform](./projects/scada-data-platform/)

Industrial telemetry architecture for operational technology environments.

**Topics**

* SCADA
* Industrial IoT
* Asset Monitoring
* Operational Analytics

---

### [synthetic-iot-data-generator](./projects/synthetic-iot-data-generator/)

Framework for generating realistic industrial telemetry and operational events.

**Topics**

* Synthetic Data
* Time-Series Simulation
* AI Training Data
* Architecture Demonstrations

---

## 2. Medallion Architecture Frameworks

### [raw-to-enriched-framework](./projects/raw-to-enriched-framework/)

Reusable ingestion and standardization framework.

**Topics**

* Bronze Layer
* Data Standardization
* Incremental Processing
* Metadata-Driven Pipelines

---

### [enriched-to-curated-framework](./projects/enriched-to-curated-framework/)

Business-rule-driven transformation framework.

**Topics**

* Silver-to-Gold Processing
* Data Modeling
* Aggregations
* Curated Data Products

---

### [metadata-driven-pipeline-framework](./projects/metadata-driven-pipeline-framework/)

Metadata-driven orchestration platform used to scale large numbers of pipelines.

**Topics**

* Pipeline Automation
* Configuration-Driven Development
* Enterprise Data Engineering
* Reusable Templates

---

## 3. Governance & Metadata

### [enterprise-metadata-management](./projects/enterprise-metadata-management/)

Enterprise metadata strategy and governance architecture.

**Topics**

* Technical Metadata
* Business Metadata
* Data Lineage
* Data Governance

---

### [delta-lakehouse-governance](./projects/delta-lakehouse-governance/)

Governance patterns for Lakehouse platforms.

**Topics**

* Data Security
* Access Control
* Auditing
* Compliance

---

### [metadata-driven-vs-reference-based-architecture](./projects/metadata-driven-vs-reference-based-architecture/)

Architectural comparison between metadata-driven and traditional reference-table approaches.

**Topics**

* Architecture Tradeoffs
* Scalability
* Maintainability
* Enterprise Design

---

## 4. Data Quality & Observability

### [enterprise-data-quality-framework](./projects/enterprise-data-quality-framework/)

Enterprise-scale data quality architecture.

**Topics**

* Data Validation
* Data Profiling
* Rule Engines
* Quality Monitoring

---

### [dq-metadata-framework](./projects/dq-metadata-framework/)

Metadata-driven quality rules platform.

**Topics**

* Quality Configuration
* Rule Management
* Validation Automation
* Diagnostics

---

### [pipeline-observability-platform](./projects/pipeline-observability-platform/)

Operational monitoring platform for enterprise pipelines.

**Topics**

* Logging
* Alerting
* Monitoring
* Root Cause Analysis

---

### [databricks-monitoring-dashboard](./projects/databricks-monitoring-dashboard/)

Databricks operational dashboard architecture.

**Topics**

* Dashboard Design
* Platform Monitoring
* Operational Reporting
* Pipeline Run Analytics

---

## 5. Energy & Utility Analytics

### [energy-curation](./projects/energy-curation/)

Enterprise energy analytics curation layer.

**Topics**

* Energy Markets
* Operational Analytics
* Curated Reporting
* Lakehouse Curation

---

### [icap-curation](./projects/icap-curation/)

Installed Capacity historical and daily curation framework.

**Topics**

* Effective Dating
* SCD Processing
* Utility Analytics
* Historical Snapshot Logic

---

### [lmp-curation](./projects/lmp-curation/)

Locational Marginal Pricing curation architecture.

**Topics**

* Energy Markets
* High-Volume Processing
* Time-Series Analytics
* Daily and Historical Loads

---

## 6. Migration & Modernization

### [opr-data-migration](./projects/opr-data-migration/)

Large-scale operational data migration framework.

**Topics**

* Legacy Modernization
* Data Migration
* Validation
* Reconciliation

---

### [databricks-pipeline-migration](./projects/databricks-pipeline-migration/)

Migration methodology for modernizing enterprise data pipelines.

**Topics**

* Platform Migration
* CI/CD
* Deployment Automation
* Environment Promotion

---

### [github-migration-automation](./projects/github-migration-automation/)

Repository migration and modernization tooling.

**Topics**

* Git Automation
* DevOps
* Repository Standardization
* Migration Scripts

---

## 7. Platform Administration

### [pipeline-admin-framework](./projects/pipeline-admin-framework/)

Administrative control plane for enterprise pipeline management.

**Topics**

* Configuration Management
* Pipeline Operations
* Platform Administration
* Run Management

---

### [merge-lib-framework](./projects/merge-lib-framework/)

Reusable framework for standardized merge operations.

**Topics**

* Delta Lake
* Data Synchronization
* Reusable Components
* Merge Patterns

---

## 8. DevOps & Deployment

### [gitlab-cicd-for-databricks](./projects/gitlab-cicd-for-databricks/)

CI/CD implementation patterns for Databricks environments.

**Topics**

* GitLab
* DevOps
* Automated Deployment
* Release Management

---

### [azure-databricks-deployment-framework](./projects/azure-databricks-deployment-framework/)

Deployment architecture for enterprise Databricks environments.

**Topics**

* Environment Promotion
* Infrastructure Automation
* Platform Engineering
* Deployment Governance

---

# Architecture Focus Areas

This portfolio demonstrates practical experience in:

* Enterprise Data Platforms
* Data Lakehouse Architecture
* AI Infrastructure
* Metadata-Driven Engineering
* Industrial IoT
* SCADA Analytics
* Energy Analytics
* Platform Governance
* Data Quality
* Observability
* DevOps
* Cloud Migration
* Enterprise Architecture

---

# Technical Stack

## Data Engineering

* Azure Databricks
* Spark SQL
* PySpark
* Delta Lake
* Azure Data Factory
* Synapse Analytics
* CDC
* SCD Type 2
* Metadata-driven pipelines

## Cloud

* Azure
* AWS
* GCP

## AI

* OpenAI
* Bedrock
* LangChain
* RAG
* Vector Databases
* AI Agents

## DevOps

* GitHub
* GitLab
* CI/CD Pipelines
* Infrastructure Automation
* Environment Promotion

---

# Repository Principles

This repository intentionally focuses on:

* Architectural patterns
* Reusable frameworks
* Platform design
* Technical documentation
* Demonstration projects
* Interview- and client-friendly artifacts

rather than employer-specific implementations.

All examples have been anonymized and generalized for public sharing.

---

# License

This repository is intended for educational, professional portfolio, and knowledge-sharing purposes.

All architectures, examples, and demonstrations are provided as reference implementations and should be adapted to individual organizational requirements.
