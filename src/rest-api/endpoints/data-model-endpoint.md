---
title: Data Model
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 300
---

Introspection of the facets, schemas and document types contributed to the Nuxeo Server.

## Get All Facets

```
GET /config/facets
```

### Response Body

If successful, returns a collection of [facet entities]({{page page='facet-entity-type'}}) containing all the facets contributed to the Nuxeo Server.

### Status Codes

- 200 *OK* - Success.

## Get a Facet

```
GET /config/facets/FACET_NAME
```

### Path Parameters

| Parameter Name | Value      | Description     |
| -------------- | ---------- | --------------- |
| **FACET_NAME** | **string** | The facet name. |

### Response Body

If successful, returns a [facet entity]({{page page='facet-entity-type'}}) representing the facet with the given `FACET_NAME` path parameter.

### Status Codes

- 200 *OK* - Success.
- 204 *Not Found* - Facet with the given `FACET_NAME` path parameter not found.

## Get All Schemas

```
GET /config/schemas
```

### Response Body

If successful, returns a collection of [schema entities]({{page page='schema-entity-type'}}) containing all the schemas contributed to the Nuxeo Server.

### Status Codes

- 200 *OK* - Success.

## Get a Schema

```
GET /config/schemas/SCHEMA_NAME
```

### Path Parameters

| Parameter Name  | Value      | Description      |
| --------------- | ---------- | ---------------- |
| **SCHEMA_NAME** | **string** | The schema name. |

### Response Body

If successful, returns a [schema entity]({{page page='schema-entity-type'}}) representing the schema with the given `SCHEMA_NAME` path parameter.

### Status Codes

- 200 *OK* - Success.
- 204 *Not Found* - Schema with the given `SCHEMA_NAME` path parameter not found.

## Get All Document Types

```
GET /config/types
```

### Response Body

If successful, returns a collection of [document type entities]({{page page='document-type-entity-type'}}) containing all the document types contributed to the Nuxeo Server.
<!--
// TODO: also returns schemas
-->
### Status Codes

- 200 *OK* - Success.

## Get a Document Type

```
GET /config/types/DOC_TYPE
```

### Path Parameters

| Parameter Name | Value      | Description             |
| -------------- | ---------- | ----------------------- |
| **DOC_TYPE**   | **string** | The document type name. |

### Response Body

If successful, returns a [document type entity]({{page page='document-type-entity-type'}}) representing the document type with the given `DOC_TYPE` path parameter.

### Status Codes

- 200 *OK* - Success.
- 204 *Not Found* - Document type with the given `DOC_TYPE` path parameter not found.
