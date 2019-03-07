---
title: Directory Endpoint
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 400
---

## Get All Directories

```
GET /directory
```

### Response

If successful, returns a collection of [directory entities]({{page page='directory-entity-type'}}) containing all the directories contributed to the Nuxeo Server.

### Status Codes

- 200 *OK* - Success.

## Get a Directory's Entries

```
GET /directory/DIRECTORY_ID
```

### Path Parameters

| Parameter Name   | Value      | Description       |
| ---------------- | ---------- | ----------------- |
| **DIRECTORY_ID** | **string** | The directory id. |

### Response

If successful, returns a collection of [directory entry entities]({{page page='directory-entry-entity-type'}}) containing all the entries of the directory with the given `DIRECTORY_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 204 *Not Found* - Directory with the given `DIRECTORY_ID` path parameter not found.

## Create a Directory Entry

```
POST /directory/DIRECTORY_ID/
```

### Path Parameters

| Parameter Name   | Value      | Description       |
| ---------------- | ---------- | ----------------- |
| **DIRECTORY_ID** | **string** | The directory id. |

### Request Body

Supply a [directory entry entity]({{page page='directory-entry-entity-type'}}) representing the directory entry to create with the following properties:

| Property Name     | Value      | Description                                                           |
| ----------------- | ---------- | --------------------------------------------------------------------- |
| **entity-type**   | **string** | Value: the fixed string `"directoryEntry"`.                           |
| **directoryName** | **string** | The directory name.                                                   |
| **properties**    | **object** | A collection of key-value pairs of directory entry properties to set. |
| **properties.id** | **string** | The directory entry id.                                               |

### Response

If successful, returns a [directory entry entity]({{page page='directory-entry-entity-type'}}) representing the created directory entry.

### Status Codes

- 201 *Created* - Success.
- 404 *Not Found* - Directory with the given `DIRECTORY_ID` path parameter not found.
- 500 *Internal Server Error* - Directory with the given `directoryName` property not found or directory entry with the given `properties.id` property exists.

## Get a Directory Entry

```
GET /directory/DIRECTORY_ID/ENTRY_ID
```

### Path Parameters

| Parameter Name   | Value      | Description             |
| ---------------- | ---------- | ----------------------- |
| **DIRECTORY_ID** | **string** | The directory id.       |
| **ENTRY_ID**     | **string** | The directory entry id. |

### Response

If successful, returns a [directory entry entity]({{page page='directory-entry-entity-type'}}) representing the directory entry with the given `ENTRY_ID` path parameter in the directory with the given `DIRECTORY_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Directory with the given `DIRECTORY_ID` path parameter or directory entry with the given `ENTRY_ID` path parameter not found.

## Update a Directory Entry

```
PUT  /directory/DIRECTORY_ID/ENTRY_ID
```

### Path Parameters

| Parameter Name   | Type       | Description             |
| ---------------- | ---------- | ----------------------- |
| **DIRECTORY_ID** | **string** | The directory id.       |
| **ENTRY_ID**     | **string** | The directory entry id. |

### Request Body

Supply a [directory entry entity]({{page page='directory-entry-entity-type'}}) representing the directory entry to update with the following properties:

| Property Name     | Type       | Description                                                              |
| ----------------- | ---------- | ------------------------------------------------------------------------ |
| **entity-type**   | **string** | Value: the fixed string `"directoryEntry"`.                              |
| **directoryName** | **string** | The directory name.                                                      |
| **id**            | **string** | The directory entry id.                                                  |
| **properties**    | **object** | A collection of key-value pairs of directory entry properties to update. |

### Response

If successful, returns a [directory entry entity]({{page page='directory-entry-entity-type'}}) representing the updated directory entry.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Directory with the given `DIRECTORY_ID` path parameter or directory entry with the given `ENTRY_ID` path parameter not found.
- 500 *Internal Server Error* - Directory with the given `directoryName` property not found or directory entry with the given `properties.id` not found.

## Delete a Directory Entry

```
DELETE /directory/DIRECTORY_ID/ENTRY_ID
```

### Path Parameters

| Parameter Name   | Type       | Description             |
| ---------------- | ---------- | ----------------------- |
| **DIRECTORY_ID** | **string** | The directory id.       |
| **ENTRY_ID**     | **string** | The directory entry id. |

### Response

If successful, removes the directory entry with the given `ENTRY_ID` path parameter from the directory with the given `DIRECTORY_ID` path paramater.

### Status Codes

- 204 *No Content* - Success.
- 404 *Not Found* - Directory with the given `DIRECTORY_ID` path parameter or directory entry with the given `ENTRY_ID` path parameter not found.
