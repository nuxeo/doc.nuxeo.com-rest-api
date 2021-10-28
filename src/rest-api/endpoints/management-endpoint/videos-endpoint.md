---
title: Videos Endpoint
review:
  comment: ''
  date: '2021-10-26'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 800
---

## Recompute Video Conversions

```
POST /management/videos/recompute
```

### Body Parameters

| Parameter Name            | Type        | Description                                                                                 | Notes    |
| ------------------------- | ----------- | ------------------------------------------------------------------------------------------- | -------- |
| **query**                 | **string**  | An NXQL query.                                                                              | Optional |
| **conversionNames**       | **string**  | One or several conversion names to recompute                                                | Optional |
| **recomputeAllVideoInfo** | **boolean** | Whether or not to recompute all video info. Only missing info will be recomputed if `false` | Optional |

The `query` defaults to:

```
SELECT * FROM Document
  WHERE ecm:mixinType = 'Video' AND ecm:isProxy = 0
    AND ecm:isVersion = 0 AND vid:transcodedVideos/0/name IS NULL
```

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the recompute bulk action.

The recompute status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes\*\*

- 200 _OK_ - Success.

### Sample

To recompute the video conversions for the documents matching a given query:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/videos/recompute \
-d 'query=SELECT * FROM Document WHERE ecm:mixinType = "Video"'
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "93baf453-5d34-4bb9-9370-54ec4cce78b2",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "recomputeVideoConversion",
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
