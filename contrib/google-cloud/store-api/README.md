# Introduction

This is a lightweight api service to store and retrieve AppThreat scan reports.

Health check

```bash
curl http://url/healthcheck
```

Post summary data

```bash
curl --header "Content-Type: application/json" -d '{"id": "foo", "data": "bar"}' http://url/summary
```

Upload scan report

```bash
curl -F 'file=@/Users/prabhu/Downloads/CodeAnalysisLogs/scan-full-report.json' http://0.0.0.0:8080/scans
```

Retrieve scans

By scan id (SARIF -> runs -> automationDetails.guid)

```bash
curl http://0.0.0.0:8080/scans?id=c3983af9-7dc0-4a6e-8109-726ee127530d
```

```bash
curl "http://0.0.0.0:8080/scans?repositoryUri=https://github.com/AppThreat/WebGoat&branch=develop"
```

Delete scans

```bash
curl -X DELETE "http://0.0.0.0:8080/scans?repositoryUri=https://github.com/AppThreat/WebGoat&branch=develop&revisionId=210dbaf5f0f49a79cb1adf9760c36658c819ff7d"
```

## Integration with Datastudio

```bash
gcloud firestore export gs://at_scans --collection-ids=at_scans
```

```bash
bq --location=US load \
--source_format=DATASTORE_BACKUP \
--replace \
at_scans_analysis.all_apps \
gs://at_scans/path/.export_metadata
```

Eg:

```
gs://at_scans/2021-07-21T13:22:42_29189/all_namespaces/kind_at_scans/all_namespaces_kind_at_scans.export_metadata
```
