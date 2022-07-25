---
title: Group
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 700
---

Group CRUD.

## Create a Group

```
POST /group
```

### Request Body

Supply a [group entity]({{page page='group-entity-type'}}) representing the group to create with the following properties:

| Property Name   | Value      | Description                                                 | Notes    |
| --------------- | ---------- | ----------------------------------------------------------- | -------- |
| **entity-type** | **string** | Value: the fixed string `"group"`.                          |          |
| **id**          | **object** | The group id.                                               |          |
| **properties**  | **object** | A collection of key-value pairs of group properties to set. | Optional |

### Response

If successful, returns a [group entity]({{page page='group-entity-type'}}) representing the created group.

### Status Codes

- 201 *Created* - Success.
- 409 *Conflict* - Group with the given `id` property exists.

## Get a Group

```
GET /group/GROUP_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **GROUP_ID**   | **string** | The group id. |

### Response

If successful, returns a [group entity]({{page page='group-entity-type'}}) representing the group with the given `GROUP_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Group with the given `GROUP_ID` path parameter not found.

## Update a Group

```
PUT /group/GROUP_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **GROUP_ID**   | **string** | The group id. |

### Request Body

Supply a [group entity]({{page page='group-entity-type'}}) representing the group to update with the following properties:

| Property Name   | Type       | Description                                                    | Notes    |
| --------------- | ---------- | -------------------------------------------------------------- | -------- |
| **entity-type** | **string** | Value: the fixed string `"group"`.                             |          |
| **id**          | **string** | The group id.                                                  |          |
| **properties**  | **object** | A collection of key-value pairs of group properties to update. | Optional |

### Response

If successful, returns a [group entity]({{page page='group-entity-type'}}) representing the updated group.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Group with the given `GROUP_ID` path parameter not found.
- 500 *Internal Server Error* - Group with the given `id` property not found.

## Delete a Group

```
DELETE /group/GROUP_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **GROUP_ID**   | **string** | The group id. |

### Response

If successful, deletes the group with the given `GROUP_ID` path parameter.

### Status Codes

- 204 *No Content* - Success.
- 404 *Not Found* - User with the given `GROUP_ID` path parameter not found.

## Add a User to a Group

```
POST /group/GROUP_ID/user/USER_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **GROUP_ID**   | **string** | The group id. |
| **USER_ID**    | **string** | The user id.  |

### Response

If successful, returns a [group entity]({{page page='group-entity-type'}}) representing the group with the given `GROUP_ID` path parameter to which was added the user with the given `USER_ID` path parameter.

### Status Codes

- 201 *Created* - Success.
- 404 *Not Found* - Group with the given `GROUP_ID` path parameter or user with the given `USER_ID` path parameter not found.

## Remove a User from a Group

```
DELETE /group/GROUP_ID/user/USER_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **GROUP_ID**   | **string** | The group id. |
| **USER_ID**    | **string** | The user id.  |

### Response

If successful, removes the user with the given `USER_ID` path parameter from the group with the given `GROUP_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - Group with the given `GROUP_ID` path parameter or user with the given `USER_ID` path parameter not found.
