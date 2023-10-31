---
title: Thumbnails Endpoint
review:
  comment: ''
  date: '2021-10-26'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 700
---

## Recompute Thumbnails

```
POST /management/thumbnails/recompute
```

### Body Parameters

| Parameter Name | Type       | Description                                 | Notes    |
| -------------- | ---------- | ------------------------------------------- | -------- |
| **query**      | **string** | An NXQL query to select a set of documents. | Optional |

The `query` defaults to:

```
SELECT * FROM Document
  WHERE ecm:mixinType = 'Thumbnail' AND thumb:thumbnail/data IS NULL
    AND ecm:isVersion = 0 AND ecm:isProxy = 0 AND ecm:isTrashed = 0
```

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the recompute bulk action.

The recompute status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.
- 409 *Conflict* - A recompute with an empty query is already in progress.

### Sample

To recompute the thumbnails for the documents matching a given query:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/thumbnails/recompute \
-d 'query=SELECT * FROM Document WHERE ecm:mixinType = "Thumbnail"'
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "0e1e6800-631a-4e04-a47c-241ea7b3596a",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "recomputeThumbnails",
  "username": "system",
  "submitted": "2019-07-26T12:13:31.361Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```
