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

| Parameter Name | Type       | Description     | Notes                                                  |
| -------------- | ---------- | --------------- |--------------------------------------------------------|
| **query**      | **string** | The NXQL query. | Optional, no query means reindex the entire repository |

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the index bulk action.

The index status can be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 *OK* - Success.
- 409 *Conflict* - A repository reindex is already in progress.

### Sample

To reindex the `foobar` repository, this will create a new index (applying settings and mappings):

```curl
curl -X POST -u Administrator:Administrator \
-H "X-NXRepository: foobar" \
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

## Optimize the Repository Index

```
POST /management/elasticsearch/optimize
```

### Status Codes

- 204 *No Content* - Success.

### Sample

To optimize the `default` repository index:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/elasticsearch/optimize

```

Note that this endpoint is now called [`_forcemerge`](https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-forcemerge.html) in Elastic.

## Check for search Desynchronisation between Elastic and the Repository

```
GET /management/elasticsearch/checkSearch
```

### Query Parameters

| Parameter Name | Type       | Description                         | Notes                                           |
|----------------|------------|-------------------------------------|-------------------------------------------------|
| **nxql**       | **string** | The NXQL query.                     | Optional, no query means all visible documents  |
| **pageSize**   | **number** | The number of documents to return.  | Optional, default is 10                         |

### Response

If successful, returns a JSON response containing information about the search results from 2 page providers: `repo` and
`elastic`.

The `repo` result is run against repository backend using `nxql_repo_search` page provider, while the `elastic` is run
against `nxql_elastic_search` page provider.

Note that only document identifiers are returned, this is on purpose because management endpoint should not expose
document content.

### Status Codes

- 200 *OK* - Success.

### Sample

To check the number of visible documents in Elastic and in the repository:

```curl
curl -X GET -u Administrator:Administrator \
   --data-urlencode "nxql=SELECT * FROM Document WHERE ecm:isProxy = 0 AND ecm:isVersion = 0 AND ecm:isTrashed = 0" \
   --data-urlencode "pageSize=5" \
   http://localhost:8080/nuxeo/api/v1/management/elasticsearch/checkSearch
```

```json
{
  "query": "SELECT * FROM Document WHERE ecm:isProxy = 0 AND ecm:isVersion = 0 AND ecm:isTrashed = 0",
  "order": {
    "sortColumn": "dc:modified",
    "sortAscending": false
  },
  "repo": {
    "took": 324,
    "resultsCount": 99891,
    "pageSize": 5,
    "pageProvider": "nxql_repo_search",
    "resultsCountLimit": 0,
    "result": [
      "545cb06b-3cef-428d-a9b8-a6069f2254c0",
      "373b3f32-ba4b-4ebd-b660-fd1385c78d59",
      "0755d7dc-e8b3-4610-805e-5d3bc60d8c77",
      "ac811414-7480-416f-a958-45b6a775a0f3",
      "7ec69eeb-0f28-4fed-befc-8598801e0b07"
    ]
  },
  "elastic": {
    "took": 22,
    "resultsCount": 99891,
    "pageSize": 5,
    "pageProvider": "nxql_elastic_search",
    "resultsCountLimit": 10000,
    "result": [
      "545cb06b-3cef-428d-a9b8-a6069f2254c0",
      "373b3f32-ba4b-4ebd-b660-fd1385c78d59",
      "0755d7dc-e8b3-4610-805e-5d3bc60d8c77",
      "7ec69eeb-0f28-4fed-befc-8598801e0b07",
      "ac811414-7480-416f-a958-45b6a775a0f3"
    ]
  }
}
```

If there are discrepancies, further investigation can be done using directly the page providers (`nxql_repo_search` or `nxql_elastic_search`).

```curl
curl -X GET -u Administrator:Administrator \
   --data-urlencode "queryParams=SELECT * FROM Document WHERE ecm:isProxy = 0 AND ecm:isVersion = 0 AND ecm:isTrashed = 0" \
   --data-urlencode "pageSize=5" \
   http://localhost:8080/nuxeo/api/v1/search/pp/nxql_repo_search/execute
```

## Learn More

- [Elasticsearch Setup]({{page version='' space='nxdoc' page='elasticsearch-setup'}}).
