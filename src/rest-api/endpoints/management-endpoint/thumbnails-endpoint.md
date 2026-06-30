---
title: Thumbnails Endpoint
review:
  comment: ''
  date: '2026-06-30'
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

## Remove Thumbnails

```
DELETE /management/thumbnails/remove
```

Removes the thumbnail blob and the `Thumbnail` facet from documents matching the given query. Available since `2025.22`.

This endpoint is intended to reclaim storage. Typical use cases include:

- Purging thumbnails from archive workspaces or any set of documents that no longer needs them.
- Cleaning up existing thumbnails on repositories where thumbnail auto-generation has been disabled (see the [nuxeo.thumbnail.enabled]({{page page='configuration-parameters-index-nuxeoconf'}}#nuxeothumbnailenabled) configuration property and the [thumbnailConfiguration]({{page page='thumbnail'}}#disabling-thumbnail-auto-generation) extension point on the `ThumbnailService`).

{{#> callout type='warning' heading='Heavy operation'}}
This is a heavy `DELETE` operation, backed by the [Bulk Action Framework]({{page space='nxdoc' page='bulk-action-framework'}}):

- The NXQL `query` should be carefully scoped to the documents actually targeted.
- The underlying `removeThumbnails` bulk action can be tuned in `nuxeo.conf` through the standard bulk action parameters (`nuxeo.bulk.action.removeThumbnails.defaultConcurrency` and `nuxeo.bulk.action.removeThumbnails.defaultPartitions`).
- The blob garbage collector will be stressed by the resulting orphaned blobs.

{{/callout}}

### Query Parameters

| Parameter Name | Type       | Description                                                      | Notes                          |
| -------------- | ---------- | ---------------------------------------------------------------- | ------------------------------ |
| **query**      | **string** | An NXQL query to select the documents whose thumbnail to remove. | Optional                       |
| **queryLimit** | **long**   | Maximum number of documents to process.                          | Optional, default is unlimited |

The `query` defaults to:

```
SELECT * FROM Document
  WHERE ecm:mixinType = 'Thumbnail' AND thumb:thumbnail/data IS NOT NULL
    AND ecm:isProxy = 0
```

Versioned and trashed documents are intentionally included in the default query to maximize storage reclamation.

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the remove bulk action.

The remove status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.
- 409 *Conflict* - A remove with an empty query is already in progress.

### Sample

To remove the thumbnails for all eligible documents in the repository:

```curl
curl -X DELETE -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/thumbnails/remove
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "1a2b3c4d-5e6f-7a8b-9c0d-1e2f3a4b5c6d",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "removeThumbnails",
  "username": "system",
  "submitted": "2026-06-30T10:00:00.000Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```

To remove the thumbnails for a custom set of documents, capped at 10,000 documents:

```curl
curl -X DELETE -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/thumbnails/remove?query=SELECT+*+FROM+Document+WHERE+ecm:path+STARTSWITH+'/default-domain/workspaces/archived'&queryLimit=10000"
```
