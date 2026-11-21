# Data Ingestion

| Path | Implementation |
| --- | --- |
| Historical CSVs | [Dataset pack](../Datasets/README.md) → [Databricks notebook](Batch/01_Shipments_Batch.scala) or [portable Spark batch](Batch/meridian-batch.scala) |
| Tracking fixture | [Keyed fixture](../Datasets/streaming/tracking_events_kafka_keyed.txt) → [Kafka producer image](../Development/Docker/meridian-producer.Dockerfile) → [broker](../Development/Kubernetes/meridian-kafka.yaml) |
| Live consumption | [Spark consumer](Streaming/meridian-stream.scala) → Iceberg replay, Delta audit, and Iceberg windows |
| Tracking export audit | [43-event JSONL export](../Datasets/streaming/meridian-kafka-events.jsonl) → tracking audit cells in the [Databricks notebook](Batch/01_Shipments_Batch.scala) |

The finite local replay starts from one partition. Use a fresh topic and matching checkpoint for independent runs. [Setup instructions](../README.md#run-the-kubernetes-replay)
