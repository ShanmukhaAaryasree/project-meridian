# Testing and Evidence

| Check | Evidence |
| --- | --- |
| Historical data quality | [Shipment reconciliation](../meridian-batch-kubernetes.log) and [malformed ID and Delta upsert regression](../evidence/meridian-delta-upsert-verification.log) |
| KPI formats | [Delta and Iceberg parity](../evidence/databricks-kpi-comparison.csv) |
| Iceberg schema evolution | [14 before and 14 after](../evidence/databricks-schema-evolution-row-counts.png) |
| ADLS storage and recovery | [Read/write probe](../meridian-adls-write-verification.log) and [pod recovery and snapshot comparison](../meridian-adls-recovery-verification.log) |
| Kubernetes operations | [Rolling update and rollback](../evidence/kubernetes-producer-rollout.log) |
| Hosted CI | [Workflow source](../.github/workflows/ci.yml) and [latest runs on main](https://github.com/ShanmukhaAaryasree/project-meridian/actions/workflows/ci.yml?query=branch%3Amain) |

The [local validation script](../validate-project.ps1) checks the producer image and archived batch and streaming results. See the [requirements matrix](../docs/requirements-compliance.md#verification-scope) for the verification scope and limitations.
