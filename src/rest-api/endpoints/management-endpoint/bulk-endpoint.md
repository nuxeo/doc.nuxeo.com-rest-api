---
title: Bulk Endpoint
review:
  comment: ''
  date: '2021-10-26'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 200
---

## Get a Bulk Action Status

```
GET /management/bulk/COMMAND_ID
```

### Path Parameters

| Parameter Name | Type       | Description     |
| -------------- | ---------- | --------------- |
| **COMMAND_ID** | **string** | The command id. |

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status with the given `COMMAND_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Command with the given `COMMAND_ID` does not exist.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/bulk/0e1e6800-631a-4e04-a47c-241ea7b3596a
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

## Learn More

- [Bulk REST API]({{page page='bulk-action-framework'}}#bulk-rest-api).
