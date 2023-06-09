---
title: Blobs Endpoint
review:
    comment: ''
    date: '2023-05-15'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 150
---

## Garbage Collect Document's Blobs

```
DELETE /management/blobs/orphaned
```

Garbage collect all the orphaned document's blobs (which are not referenced by any documents anymore). Available since `2021.38`.

### Query Parameters

| Parameter Name | Type        | Description                     | Notes                      |
| -------------- | ----------- | ------------------------------- | -------------------------- |
| **dryRun**     | **boolean** | Do not effectively delete blobs | Optional, default is false |

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the garbage collection bulk action.

The garbage collection can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.
- 501 *OK* - Not implemented.

This garbage collection is only implemented on instances working with:
 - repositories having the `ecm:blobKeys` capability (introduced by https://jira.nuxeo.com/browse/NXP-29516) i.e. MongoDB
 - blob providers extending [BlobStoreBlobProvider](https://community.nuxeo.com/api/nuxeo/latest/javadoc/org/nuxeo/ecm/core/blob/BlobStoreBlobProvider.html) such as [S3BlobProvider](https://community.nuxeo.com/api/nuxeo/latest/javadoc/org/nuxeo/ecm/blob/s3/S3BlobProvider.html) and [LocalBlobProvider](https://community.nuxeo.com/api/nuxeo/latest/javadoc/org/nuxeo/ecm/core/blob/LocalBlobProvider.html)

### Sample

Invoke GC:
```curl
curl -X DELETE -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/blobs/orphaned
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "09361005-59a9-4f00-9ff1-78de52988eb5",
  "state": "SCHEDULED",
  "processed": 0,
  "skipCount": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "garbageCollectOrphanBlobs",
  "username": "system",
  "submitted": "2023-05-15T16:24:00.863Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```

Then monitor the GC with:
```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/bulk/09361005-59a9-4f00-9ff1-78de52988eb5
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "09361005-59a9-4f00-9ff1-78de52988eb5",
  "state": "COMPLETED",
  "processed": 79,
  "skipCount": 78,
  "error": false,
  "errorCount": 0,
  "total": 79,
  "action": "garbageCollectOrphanBlobs",
  "username": "system",
  "submitted": "2023-05-15T16:54:50.345Z",
  "scrollStart": "2023-05-15T16:54:50.431Z",
  "scrollEnd": "2023-05-15T16:54:50.675Z",
  "processingStart": "2023-05-15T16:54:50.702Z",
  "processingEnd": "2023-05-15T16:54:50.805Z",
  "completed": "2023-05-15T16:54:50.843Z",
  "processingMillis": 103,
  "result": {
    "totalSize": 8942206,
    "deletedSize": 11210,
    "dryRun": false
  }
}
```
where:
 - `processed` is the total count of scrolled blobs from the blob provider(s) of the repository
 - `skipCount` is the total count of blobs that were not GC (because still referenced in the repository)
 - `processed` - `skipCount` is the total count of blobs that were garbage collected i.e. detected as orphaned (here 79-78 = 1 blob)
 - `result.totalSize` is the sum of the size of all the scrolled blob from the blob provider(s) of the repository in bytes (here ~8 MB)
 - `result.deletedSize` is the sum of the size of the blobs that were garbage collected in bytes (here ~10 KB)
 - `dryRun` whether the blobs were effectively deleted

 ## Learn More

- [Garbage-Collecting Orphaned Blobs]({{page space='nxdoc' page='garbage-collecting-orphaned-blobs'}}).
