# Logging and Monitoring

| Evidence | What to look for |
| --- | --- |
| [Kubernetes batch log](meridian-batch-kubernetes.log) | `Batch verified` and the shipment reconciliation |
| [Local replay](meridian-stream-before-restart.log) and [restart](meridian-stream-after-restart.log) | 43 saved events and the same 12 windows after restart |
| [ADLS recovery log](meridian-adls-recovery-verification.log) | 44 restored records, one new event, and the final 45-record audit |
| [Kafka lag measurement](../Testing/evidence/meridian-kafka-lag.csv) | Committed Spark and Kafka end offsets both at 45 |
| [Producer rollout](../Testing/evidence/kubernetes-producer-rollout.log) | Deployment update, rollback, and readiness |
| [Fresh rerun attempt](../Testing/evidence/meridian-final-demo-attempt.log) | Local Docker Desktop timeout before the ADLS stage |

The [lag utility](../Development/Scripts/measure-meridian-kafka-lag.ps1) compares committed Spark offsets with broker end offsets. See the [demo guide](../docs/demo-guide.md#inspect-a-failed-deployment) for inspecting Kubernetes logs and events.
