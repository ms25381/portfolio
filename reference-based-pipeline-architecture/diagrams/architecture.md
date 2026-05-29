# Reference-Based Pipeline Architecture Diagram

```text
                         REFERENCE-BASED PIPELINE ARCHITECTURE

                                      +----------------------+
                                      |      PIPELINE        |
                                      |  Central Registry    |
                                      +----------+-----------+
                                                 |
                                                 |
                              references explicit component IDs
                                                 |
              +----------------------------------+----------------------------------+
              |                                  |                                  |
              v                                  v                                  v

+-----------------------------+    +-----------------------------+    +-----------------------------+
|     PARAMETER SCHEMA        |    |      PIPELINE TEMPLATE      |    |   PIPELINE ORCHESTRATION    |
|     Schema Contract         |    |      Execution Flow         |    |   Schedule / Triggers        |
+-------------+---------------+    +-------------+---------------+    +-------------+---------------+
              |                                  |                                  |
              |                                  v                                  |
              |                   +-----------------------------+                  |
              |                   |     PARAMETER VALUES        |                  |
              |                   |     Runtime Configuration   |                  |
              |                   +-------------+---------------+                  |
              |                                  |                                  |
              +----------------------------------+----------------------------------+
                                                 |
                                                 v
                                      +----------------------+
                                      |   VALIDATED PLAN     |
                                      |   Execution Plan     |
                                      +----------+-----------+
                                                 |
                                                 v
                                      +----------------------+
                                      |  PIPELINE RUNTIME    |
                                      |  Databricks / Spark  |
                                      +----------+-----------+
                                                 |
                                                 v
                                      +----------------------+
                                      |   TARGET OUTPUTS     |
                                      |   Delta Tables       |
                                      +----------------------+
