# Legacy vs Reference-Based Architecture

## Purpose

This diagram compares a traditional tightly coupled metadata-driven architecture with the proposed reference-based pipeline architecture.

The goal is to show how separating responsibilities improves maintainability, governance, reuse, and long-term platform scalability.

---

## Legacy Metadata-Driven Model

```text
                  LEGACY METADATA MODEL

                 +----------------------+
                 |   METADATA TABLE     |
                 |  One Table Controls  |
                 |  Too Many Concerns   |
                 +----------+-----------+
                            |
        +-------------------+-------------------+
        |                   |                   |
        v                   v                   v

+---------------+   +---------------+   +---------------+
| Pipeline      |   | Execution     |   | Runtime       |
| Identity      |   | Logic         |   | Parameters    |
+---------------+   +---------------+   +---------------+

        |                   |                   |
        v                   v                   v

+---------------+   +---------------+   +---------------+
| Validation    |   | Scheduling    |   | Environment   |
| Rules         |   | Rules         |   | Overrides     |
+---------------+   +---------------+   +---------------+
