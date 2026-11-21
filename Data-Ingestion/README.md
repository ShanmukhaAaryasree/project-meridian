# Data Ingestion

| Path | Implementation |
| --- | --- |
| Historical CSVs | [Dataset pack](../Logistics/Data/README.md) → [Databricks notebook](../01_Shipments_Batch.scala) or [portable Spark batch](../meridian-batch.scala) |
| Tracking fixture | [Keyed fixture](../Logistics/Data/streaming/tracking_events_kafka_keyed.txt) → [Kafka producer image](../meridian-producer.Dockerfile) → [broker](../meridian-kafka.yaml) |
| Live consumption | [Spark consumer](../meridian-stream.scala) → Iceberg replay, Delta audit, and Iceberg windows |
| Tracking export audit | [43-event JSONL export](../meridian-kafka-events.jsonl) → tracking audit cells in the [Databricks notebook](../01_Shipments_Batch.scala) |

The finite local replay starts from one partition. Use a fresh topic and matching checkpoint for independent runs. [Setup instructions](../README.md#run-the-kubernetes-replay)
