---
title: Workflows Endpoint
review:
    comment: ''
    date: '2023-03-13'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 850
---

## Garbage Collect Workflows

```
DELETE /management/workflows/orphaned
```

Garbage collect all the orphaned workflows (for which all associated documents have been removed) as well as workflows in state 'done' or 'canceled'.

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the garbage collection bulk action.

The recompute status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.

### Sample

```curl
curl -X DELETE -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/workflows/orphaned
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
  "action": "garbageCollectWokflows",
  "username": "system",
  "submitted": "2023-02-26T12:13:31.361Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```
