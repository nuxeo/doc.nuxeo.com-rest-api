---
title: Elasticsearch Endpoint
review:
  comment: ''
  date: '2021-10-26'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 400
---

The Elasticsearch endpoint works with the `default` repository if none is specified. The repository can be changed using the [Repository header]({{page version='' space='nxdoc' page='special-http-headers'}}#repository).

## Reindex a Repository or a Set of Documents

```
POST /management/elasticsearch/reindex
```

### Query Parameters

| Parameter Name | Type       | Description     | Notes    |
| -------------- | ---------- | --------------- | -------- |
| **query**      | **string** | The NXQL query. | Optional |

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the index bulk action.

The index status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.

### Sample

To reindex the `foobar` repository:

```curl
curl -X POST -u Administrator:Administrator \
-H "Repository: foobar" \
http://localhost:8080/nuxeo/api/v1/management/elasticsearch/reindex
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "d3bc0a81-b061-447f-b307-c3db78b5f457",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "index",
  "username": "system",
  "submitted": "2019-07-26T14:12:29.224Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```

To reindex a set of documents on a given Nuxeo repository matching the [NXQL]({{page version='' space='nxdoc' page='nxql'}}) query:</br>
`SELECT * FROM Document WHERE dc:title LIKE 'My Title%'`

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/elasticsearch/reindex?query=SELECT+%2A+FROM+document+WHERE+dc%3Atitle+LIKE+%27My+Title%25%27%27
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "90037d73-ed19-48cc-a4ad-09f3999cf014",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "index",
  "username": "system",
  "submitted": "2019-07-26T09:26:08.761Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```

## Reindex a Document and Its Children Recursively

```
POST /management/elasticsearch/DOC_ID/reindex
```

### Path Parameters

| Parameter Name      | Type       | Description          |
| ------------------- | ---------- | -------------------- |
| **DOC_ID**          | **string** | The document Id.     |

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the index bulk action.

The index status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.

### Sample

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/elasticsearch/1fa9d3fa-04cc-4956-bc6c-8317b803e131/reindex
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "f37503d3-51b2-462e-8f1e-fa240fafa861",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "index",
  "username": "system",
  "submitted": "2019-07-26T09:45:09.874Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```

## Flush a Repository

```
POST /management/elasticsearch/flush
```

### Status Codes

- 204 *No Content* - Success.

### Sample

To flush the `default` repository:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/elasticsearch/flush
```

## Optimize a Repository

```
POST /management/elasticsearch/optimize
```

### Status Codes

- 204 *No Content* - Success.

### Sample

To optimize the `default` repository:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/elasticsearch/optimize

```

## Learn More

- [Elasticsearch Setup]({{page version='' space='nxdoc' page='elasticsearch-setup'}}).
