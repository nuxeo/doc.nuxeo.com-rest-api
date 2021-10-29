---
title: Binaries Endpoint
review:
    comment: ''
    date: '2021-10-26'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 100
---

## Garbage Collect Orphaned (unused) Binaries

```
DELETE /management/binaries/orphaned
```

### Response

If successful, returns a JSON representation of the binary manager status.

### Status Codes

- 200 *OK* - Success.
- 409 *Conflict* - Garbage collection is already in progress.

### Sample

```curl
curl -X DELETE -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/binaries/orphaned
```

```json
{
    "gcDuration": 6,
    "numBinaries": 1,
    "sizeBinaries": 4451,
    "numBinariesGC": 0,
    "sizeBinariesGC": 0,
    "gcduration": 6
}
```

## Learn More

- [Garbage-Collecting Orphaned Binaries]({{page version='' space='nxdoc' page='garbage-collecting-orphaned-binaries'}}).
