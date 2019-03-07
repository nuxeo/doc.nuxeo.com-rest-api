---
title: User Endpoint
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 1100
---

User CRUD.

## Create a User

```
POST /user
```

### Request Body

Supply a [user entity]({{page page='user-entity-type'}}) representing the user to create with the following properties:

| Property Name           | Value      | Description                                                |
| ----------------------- | ---------- | ---------------------------------------------------------- |
| **entity-type**         | **string** | Value: the fixed string `"user"`.                          |
| **properties**          | **object** | A collection of key-value pairs of user properties to set. |
| **properties.username** | **string** | The user id.                                               |

<!--
TODO: replace **properties.username** by id when fixed on master, see https://jira.nuxeo.com/browse/NXP-27105
-->

### Response

If successful, returns a [user entity]({{page page='user-entity-type'}}) representing the created user.

### Status Codes

- 201 *Created* - Success.
- 409 *Conflict* - User with the given `properties.username` property exists.

## Get a User

```
GET /user/USER_ID
```

### Path Parameters

| Parameter Name | Type       | Description  |
| -------------- | ---------- | ------------ |
| **USER_ID**    | **string** | The user id. |

### Response

If successful, returns a [user entity]({{page page='user-entity-type'}}) representing the user with the given `USER_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - User with the given `USER_ID` path parameter not found.

## Update a User

```
PUT /user/USER_ID
```

### Path Parameters

| Parameter Name | Type       | Description  |
| -------------- | ---------- | ------------ |
| **USER_ID**    | **string** | The user id. |

### Request Body

Supply a [user entity]({{page page='user-entity-type'}}) representing the user to update with the following properties:

| Property Name   | Type       | Description                                                   | Notes    |
| --------------- | ---------- | ------------------------------------------------------------- | -------- |
| **entity-type** | **string** | Value: the fixed string `"user"`.                             |          |
| **id**          | **string** | The user id.                                                  |          |
| **properties**  | **object** | A collection of key-value pairs of user properties to update. | Optional |

### Response

If successful, returns a [user entity]({{page page='user-entity-type'}}) representing the updated user.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - User with the given `USER_ID` path parameter not found.
- 500 *Internal Server Error* - User with the given `id` property not found.

## Delete a User

```
DELETE /user/USER_ID
```

### Path Parameters

| Parameter Name | Type       | Description  |
| -------------- | ---------- | ------------ |
| **USER_ID**    | **string** | The user id. |

### Response

If successful, deletes the user with the given `USER_ID` path parameter.

### Status Codes

- 204 *No Content* - Success.
- 404 *Not Found* - User with the given `USER_ID` path parameter not found.

## Add a User to a Group

```
POST /user/USER_ID/group/GROUP_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **USER_ID**    | **string** | The user id.  |
| **GROUP_ID**   | **string** | The group id. |

### Response

If successful, returns a [user entity]({{page page='user-entity-type'}}) representing the user with the given `USER_ID` path parameter added to the group with the given `GROUP_ID` path parameter.

### Status Codes

- 201 *Created* - Success.
- 404 *Not Found* - User with the given `USER_ID` path parameter or group with the given `GROUP_ID` path parameter not found.

## Remove a User from a Group

```
DELETE /user/USER_ID/group/GROUP_ID
```

### Path Parameters

| Parameter Name | Type       | Description   |
| -------------- | ---------- | ------------- |
| **USER_ID**    | **string** | The user id.  |
| **GROUP_ID**   | **string** | The group id. |

### Response

If successful, removes the user with the given `USER_ID` path parameter from the group with the given `GROUP_ID` path parameter.

### Status Codes

- 200 *OK* - Success.
- 404 *Not Found* - User with the given `USER_ID` path parameter or group with the given `GROUP_ID` path parameter not found.
