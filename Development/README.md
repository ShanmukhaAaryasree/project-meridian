# Development and Deployment

| Workload | Source | Image | Kubernetes |
| --- | --- | --- | --- |
| Kafka replay producer | [Keyed data](../Logistics/Data/streaming/tracking_events_kafka_keyed.txt) | [Dockerfile](../meridian-producer.Dockerfile) | [Producer Deployment](../meridian-producer-deployment.yaml) |
| Portable Spark batch | [Scala](../meridian-batch.scala) | [Dockerfile](../meridian-batch.Dockerfile) | [Batch Job](../meridian-batch-job.yaml) |
| Spark streaming | [Scala](../meridian-stream.scala), [launcher](../meridian-stream.sh) | [Dockerfile](../meridian-stream.Dockerfile) | [Stream Deployment](../meridian-stream-deployment.yaml) |

The [Kafka manifest](../meridian-kafka.yaml) provisions the broker, Service and streaming PVC. Use the [launch script](../start-meridian-live.ps1) for a dedicated local or ADLS run. The [ADLS probe](../meridian-adls-probe.yaml) checks authenticated reads and writes. [Build and run steps](../README.md#run-the-project)
