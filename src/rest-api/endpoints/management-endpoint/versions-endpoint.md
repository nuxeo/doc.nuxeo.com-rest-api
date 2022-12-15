---
title: Versions Endpoint
review:
    comment: ''
    date: '2022-12-15'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 750
---

## Garbage Collect Orphaned Versions

```
DELETE /management/versions/orphaned
```

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the garbage collection bulk action.

The recompute status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.

### Sample

```curl
curl -X DELETE -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/versions/orphaned
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
  "action": "garbageCollectOrphanVersions",
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
