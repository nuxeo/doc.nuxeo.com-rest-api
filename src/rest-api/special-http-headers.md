---
title: Special HTTP Headers
review:
    comment: ''
    date: '2019-03-06'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 200
---

In order to have more control over REST API calls, you can use the following HTTP headers.

## depth

Control the aggregation depth.

See [Aggregating Marshallers and Avoiding Infinite Loops]({{page page='parameterizing-reusing-marshallers#aggregating-marshallers-infinite-loops'}}) for more details.

**Valid Values**

`root`, `children` and `max`.

**Default Value**

`children`.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
depth: max
```

---

## enrichers.ENTITY_TYPE

Request further information in the response.

See [(Content Enrichers)]({{page page='content-enrichers'}}) for more details.

**Valid Values**

Any contributed enricher name for the given `ENTITY_TYPE`.

Multiple enricher names must be coma separated.

**Default Value**

None.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: breadcrumb,thumbnail,children
```

---

## fetch.ENTITY_TYPE

Load additional parts of an object for the given ENTITY_TYPE.

**Valid Values**

Any extended field for the given `ENTITY_TYPE`.

Multiple fields must be coma separated.

See [Document JSON and Extended Fields]({{page page='document-json-extended-fields'}}) for more details on accepted values.

**Default Value**

None.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:creator,dc:subjects,dc:nature
```

---

## Nuxeo-Transaction-Timeout

Specify the duration of the transaction timeout in seconds.

If not provided, the value of the `nuxeo.db.transactiontimeout` configuration parameter is used. See [Configuration Parameters Index
]({{page page='configuration-parameters-index-nuxeoconf#configuration-parameters-index'}}) for more details.

**Valid Values**

Any duration in seconds greater than zero.

**Default Value**

None.

**Example**

```bash
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Nuxeo-Transaction-Timeout: 300
```

---

## nx_es_sync

Force ElasticSearch synchronous indexing during a REST call.

**Valid Values**

`true` or `false`.

**Default Value**

`false`.

**Example**

```
POST https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Content-Type: application/json
nx_es_sync: true
```

---

## properties

Filter properties so the returned document contains only data from the specified schemas.

**Valid Values**

Any schemas available on the document or `*` for all schemas.

Multiple schemas must be coma separated.

**Default Value**

None.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
properties: dublincore,file,common
```

---

## Repository

Specify the repository name if it has been changed or if you have multiple repositories.

**Valid Values**

Any contributed repository name.

**Default Value**

`default`.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Repository: other
```

---

## skipAggregates

Tell the [search endpoint]({{page version='' space='nxdoc' page='search-endpoints'}}) to skip elasticsearch aggregate computation, if any, to speed up the query.

**Valid Values**

`true` or `false`.

**Default Value**

`false`.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/search/lang/pp/PAGE_PROVIDER_NAME
skipAggregates: true
```

---

## source

Set this property in document context data to be used for automatic source-based versioning.

See [source-based versioning]({{page page='versioning#source-based-versioning'}}) for more details.

**Valid Values**

Any string value.

**Default Value**

None.

**Example**

```
POST https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Content-Type: application/json
source: REST
```

---

## X-NXVoidOperation

Force server to return no content (like a void operation).

Can be useful when dealing with blobs to avoid having the blob output sent back to the client.

**Valid Values**

`true` or `false`.

**Default Value**

`false`.

**Example**

```bash
POST https://NUXEO_SERVER/nuxeo/api/v1/automation/Document.GetBlob
Content-Type: application/json
X-NXVoidOperation: true
```

---

## X-Versioning-Option

Increment minor or major version and returns versioned document.

**Valid Values**

`NONE`, `MINOR` or `MAJOR`.

**Default Value**

`NONE`.

**Example**

```
PUT https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Content-Type: application/json
X-Versioning-Option: MAJOR
```

---
