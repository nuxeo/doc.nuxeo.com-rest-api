---
title: Document Id Endpoint
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 500
---

Document CRUD based on a document id.

## Create a Document

```
POST /id/PARENT_DOC_ID
```

### Path Parameters

| Parameter Name    | Value      | Description             |
| ----------------- | ---------- | ----------------------- |
| **PARENT_DOC_ID** | **string** | The parent document id. |

### Request Body

Supply a [document entity]({{page page='document-entity-type'}}) representing the document to create with the following properties:

| Property Name   | Value      | Description                                                    | Notes    |
| --------------- | ---------- | -------------------------------------------------------------- | -------- |
| **entity-type** | **string** | Value: the fixed string `"document"`.                          |          |
| **name**        | **string** | The document name, used as path segment.                       |          |
| **type**        | **string** | The document type.                                             |          |
| **properties**  | **object** | A collection of key-value pairs of document properties to set. | Optional |

{{#> callout type='info'}}
You don't need to specify the `uid` property since the server will create a document id. It will be part of the response body of a GET request on the created document.
{{/callout}}

### Response

If successful, returns a [document entity]({{page page='document-entity-type'}}) representing the created document.

### Status Codes

- 201 *Created* - Success.
- 404 *Not Found* - Document with the given `PARENT_DOC_ID` path parameter not found.

## Get a Document

```
GET /id/DOC_ID
```

### Path Parameters

| Parameter Name | Value      | Description      |
| -------------- | ---------- | ---------------- |
| **DOC_ID**     | **string** | The document id. |

### Response

If successful, returns a [document entity]({{page page='document-entity-type'}}) representing the document with the given `DOC_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Document with the given `DOC_ID` path parameter not found.

## Update a Document

```
PUT /id/DOC_ID
```

### Path Parameters

| Parameter Name | Value      | Description      |
| -------------- | ---------- | ---------------- |
| **DOC_ID**     | **string** | The document id. |

### Request Body

Supply a [document entity]({{page page='document-entity-type'}}) representing the document to update with the following properties:

| Property Name   | Value      | Description                                                       | Notes    |
| --------------- | ---------- | ----------------------------------------------------------------- | -------- |
| **entity-type** | **string** | Value: the fixed string `"document"`.                             |          |
| **properties**  | **object** | A collection of key-value pairs of document properties to update. | Optional |

{{#> callout type='info'}}
The `uid` property is not required but is accepted by the server. This is useful since it is part of the response body of a GET request, which you might want to reuse as a base request body for a PUT request by adapting only the properties to update.
{{/callout}}

### Response

If successful, returns a [document entity]({{page page='document-entity-type'}}) representing the updated document.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Document with the given `DOC_ID` path parameter not found.

## Delete a Document

If successful, deletes the document with the given `DOC_ID` path parameter.

{{#> callout type='warning'}}
This request performs a **permanent delete**, it doesn't put the document in the trash.
{{/callout}}

```
DELETE /id/DOC_ID
```

### Path Parameters

| Parameter Name | Value      | Description      |
| -------------- | ---------- | ---------------- |
| **DOC_ID**     | **string** | The document id. |

### Status Codes

- 204 *No Content* - Success.
- 404 *Not Found* - Document with the given `DOC_ID` path parameter not found.
