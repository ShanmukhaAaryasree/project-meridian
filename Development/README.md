# Development and Deployment

| Workload | Source | Image | Kubernetes |
| --- | --- | --- | --- |
| Kafka replay producer | [Keyed data](../Datasets/streaming/tracking_events_kafka_keyed.txt) | [Dockerfile](Docker/meridian-producer.Dockerfile) | [Producer Deployment](Kubernetes/meridian-producer-deployment.yaml) |
| Portable Spark batch | [Scala](../Data%20Ingestion/Batch/meridian-batch.scala) | [Dockerfile](Docker/meridian-batch.Dockerfile) | [Batch Job](Kubernetes/meridian-batch-job.yaml) |
| Spark streaming | [Scala](../Data%20Ingestion/Streaming/meridian-stream.scala), [launcher](../Data%20Ingestion/Streaming/meridian-stream.sh) | [Dockerfile](Docker/meridian-stream.Dockerfile) | [Stream Deployment](Kubernetes/meridian-stream-deployment.yaml) |

The [Kafka manifest](Kubernetes/meridian-kafka.yaml) provisions the broker, Service and streaming PVC. Use the [launch script](Scripts/start-meridian-live.ps1) for a dedicated local or ADLS run. The [ADLS probe](Kubernetes/meridian-adls-probe.yaml) checks authenticated reads and writes. [Build and run steps](../README.md#run-the-project)
