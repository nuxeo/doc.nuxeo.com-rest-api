---
title: OAuth2 Endpoint
review:
    comment: ''
    date: '2025-04-03'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 420
---

## Garbage Collect Expired OAuth2 Tokens

```
DELETE /management/oauth2/expired
```

Garbage collect all the expired OAuth2 tokens.

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the garbage collection bulk action.

The status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.
- 409 *Conflict* - A Garbage collect is already in progress.

### Sample

```curl
curl -X DELETE -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/oauth2/expired
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
  "action": "garbageCollectExpiredOAuth2Tokens",
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
