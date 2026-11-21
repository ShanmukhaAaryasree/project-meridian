# Project Meridian Demo Guide

1. **Architecture.** Open the README diagram. Explain how Databricks processes the CSVs and how Kubernetes runs the Kafka replay and Spark consumer.
2. **Batch quality.** Show the raw counts, the latest shipment version check, and the curated and rejected Delta outputs. Reconcile 141 input rows to 133 latest versions, then to 122 curated and 11 rejected shipments. Open `meridian-batch-kubernetes.log` for the Kubernetes Job counts and the [Delta verification log](evidence/meridian-delta-upsert-verification.log) for the update of a re-sent shipment.
3. **KPIs.** Open the monthly, carrier, lane and delay tables. Use the one-page insight summary to explain the operational findings and actions.
4. **Iceberg.** Show the four analytics tables and the added delay category column. In Spark SQL with the streaming `meridian` catalog configured, run `SELECT committed_at, snapshot_id, operation FROM meridian.tracking.event_windows.snapshots ORDER BY committed_at`. Use an earlier snapshot ID in `SELECT * FROM meridian.tracking.event_windows VERSION AS OF <snapshot_id>` and compare the rows with the current table.
5. **Recovery.** The saved local replay logs show 43 retained records and identical five-minute windows after pod replacement. The [ADLS recovery log](meridian-adls-recovery-verification.log) shows the replacement pod reading the same 44 raw records, 12 windows, 32 accepted events, and four checkpoint commits. To repeat the demonstration, seed a dedicated topic, let the consumer finish, then delete just its pod and compare its replacement's startup state. Use the same ADLS checkpoint and warehouse for both pods.
6. **Operations.** Show the producer's one- and two-replica outputs and its separate demo topic. Show the rollout, rollback, and failed deployment diagnosis. Explain that each producer replica replays the full fixture.
7. **Scope.** The consumer supports a local persistent volume and ADLS Gen2. The live Delta audit keeps event dispositions, and Databricks can produce separate audit tables from a Kafka export. The Git repository is local and the GitHub Actions workflow has not been run on a hosted runner.

Measure Kafka lag with `./measure-meridian-kafka-lag.ps1`. It compares each broker partition's end offset with the latest committed Spark checkpoint offset. Pass `-Deployment` and `-Topic` when checking another run. The [ADLS acceptance run](evidence/meridian-kafka-lag.csv) measured zero lag at offset 45.

## Inspect a failed deployment

```powershell
kubectl --context docker-desktop apply -f meridian-failure-demo.yaml
kubectl --context docker-desktop scale deployment/meridian-failure-demo --replicas=1
kubectl --context docker-desktop get pods -l app=meridian-failure-demo
kubectl --context docker-desktop logs deployment/meridian-failure-demo
kubectl --context docker-desktop describe pods -l app=meridian-failure-demo
kubectl --context docker-desktop get events --sort-by=.lastTimestamp
kubectl --context docker-desktop scale deployment/meridian-failure-demo --replicas=0
```

The container logs show the simulated missing configuration. The pod description shows exit code `42` and Kubernetes records the restart backoff in its events.
