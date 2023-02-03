---
title: Fulltext Endpoint
review:
    comment: ''
    date: '2023-02-03'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 500
---

## Extract Fulltext From Binary

```
POST /management/fulltext/extract
```

### Body Parameters

| Parameter Name | Type        | Description    | Notes    |
|----------------|-------------|----------------| -------- |
| **query**      | **string**  | An NXQL query. | Optional |
| **force**      | **boolean** | Force option.  | Optional |

The default `query` skip proxies that don't hold any fulltext and avoid to run extraction on document without downloadable binaries:

```
SELECT * FROM Document WHERE 
    ecm:isProxy = 0 AND ecm:mixinType = 'Downloadable'
```

The `force` option can be used when changing the configuration in order to nullify binary fulltext
on documents that are excluded with the new configuration. `force` is `false` by default.

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status.

The recompute status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes**

- 200 *OK* - Success.

### Sample

Run extraction of all binaries (blobs) referenced by documents, forcing nullify of existing fulltext:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/fulltext/extract -d "force=true"
```

```json
{
   "entity-type": "bulkStatus",
   "commandId": "6264cde7-03aa-4f6d-819d-960e3ef3bb12",
   "state": "SCHEDULED",
   "processed": 0,
   "error": false,
   "errorCount": 0,
   "total": 0,
   "action": "extractBinaryFulltext",
   "username": "system",
   "submitted": "2023-02-02T12:10:07.567Z",
   "scrollStart": null,
   "scrollEnd": null,
   "processingStart": null,
   "processingEnd": null,
   "completed": null,
   "processingMillis": 0
}
```

Note that in the log you will have a trace like:
```
WARN  [ExtractBinaryFulltextObject] Extracting Binary Fulltext: command: 6264cde7-03aa-4f6d-819d-960e3ef3bb12, query: SELECT * FROM Document WHERE ecm:isProxy = 0 AND ecm:mixinType = 'Downloadable', force: true
```
