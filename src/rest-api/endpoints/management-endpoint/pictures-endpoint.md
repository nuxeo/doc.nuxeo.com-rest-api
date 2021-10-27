---
title: Pictures Endpoint
review:
    comment: ''
    date: '2021-10-26'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 500
---

## Recompute Picture Views

```
POST /management/pictures/recompute
```

### Body Parameters

| Parameter Name        | Type       | Description    | Notes    |
| --------------------- | ---------- | -------------- | -------- |
| **query**             | **string** | An NXQL query. | Optional |

The `query` defaults to:

```
SELECT * FROM Document
  WHERE ecm:mixinType = 'Picture' AND picture:views/*/title IS NULL
```

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the recompute bulk action.

The recompute status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes**

- 200 *OK* - Success.

### Sample

To recompute the picture views for the documents matching a given query:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/pictures/recompute \
-d 'query=SELECT * FROM Document WHERE ecm:mixinType = "Picture"'
```

```json
{
   "entity-type": "bulkStatus",
   "commandId": "93baf453-5d34-4bb9-9370-54ec4ffe78b2",
   "state": "SCHEDULED",
   "processed": 0,
   "error": false,
   "errorCount": 0,
   "total": 0,
   "action": "recomputeViews",
   "username": "system",
   "submitted": "2019-07-26T12:10:07.567Z",
   "scrollStart": null,
   "scrollEnd": null,
   "processingStart": null,
   "processingEnd": null,
   "completed": null,
   "processingMillis": 0
}
```
