---
title: WorkManager Endpoint
review:
  comment: ''
  date: '2021-10-26'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 900
---

## Run Works in Failure

```
POST /management/work-manager/run-works-in-failure
```

### Body Parameters

| Parameter Name     | Type    | Description                            | Notes    |
| ------------------ | ------- | -------------------------------------- | -------- |
| **timeoutSeconds** | **int** | The work execution timeout in seconds. | Optional |

### Response

If successful, returns a JSON representation of the reprocessed works status.

### Status Codes

- 200 *OK* - Success.

### Sample

To specify an execution timeout:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/work-manager/run-works-in-failure
-d timeoutSeconds=10
```

```json
{
  "total": 0,
  "success": 0,
  "filtered": 0
}
```

## Learn More

- [WorkManager Dead Letter Queue]({{page page='workmanager-dql'}}).
