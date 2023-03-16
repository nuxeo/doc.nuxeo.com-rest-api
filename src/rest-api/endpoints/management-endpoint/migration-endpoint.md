---
title: Migration Endpoint
review:
  comment: ''
  date: '2023-03-16'
  status: ok
labels:
  - http
  - rest-api
  - migration
toc: true
tree_item_index: 600
---

## Get All Migration Objects

```
GET /management/migration
```

### Response

If successful, returns a JSON representation of all migration objects.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/migration
```

```json
{
  "entity-type": "migrations",
  "entries": [
    {
      "entity-type": "migration",
      "id": "trash-storage",
      "description": "Migration of in the trash storage model",
      "descriptionLabel": "migration.trash-storage",
      "status": {
        "state": "property",
        "step": null,
        "startTime": 0,
        "pingTime": 0,
        "progressMessage": null,
        "progressNum": 0,
        "progressTotal": 0,
        "running": false
      },
      "steps": []
    },
    ...and so on...
  ]
}
```

## Get Migration Object

```
GET /management/migration/MIGRATION_ID
```

### Path Parameters

| Parameter Name   | Type       | Description      |
| ---------------- | ---------- | ---------------- |
| **MIGRATION_ID** | **string** | The migration id.|

If no `MIGRATION_ID` is passed, returns all migration objects, see [Get All Migrations](#get-all-migration-objects).

### Response

If successful, returns a JSON representation of the requested migration object.

### Status Codes

- 200 _OK_ - Success.
- 404 _Not Found_ - Migration with the given `MIGRATION_ID` does not exist.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/migration/trash-storage
```

```json
{
  "entity-type": "migration",
  "id": "trash-storage",
  "description": "Migration of in the trash storage model",
  "descriptionLabel": "migration.trash-storage",
  "status": {
    "state": "property",
    "step": null,
    "startTime": 0,
    "pingTime": 0,
    "progressMessage": null,
    "progressNum": 0,
    "progressTotal": 0,
    "running": false
  },
  "steps": []
}
```

## Probe a Migration Object

```
POST /management/migration/MIGRATION_ID/probe
```

### Path Parameters

| Parameter Name   | Type       | Description      |
| ---------------- | ---------- | ---------------- |
| **MIGRATION_ID** | **string** | The migration id.|

### Response

If successful, probes the current state of a migration by analyzing persistent data, sets it as the new current state, then returns a JSON representation of the requested migration object.

### Status Codes

- 200 _OK_ - Success.
- 404 _Not Found_ - Migration with the given `MIGRATION_ID` does not exist.

### Sample

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/migration/trash-storage/probe
```

```json
{
  "entity-type": "migration",
  "id": "trash-storage",
  "description": "Migration of in the trash storage model",
  "descriptionLabel": "migration.trash-storage",
  "status": {
    "state": "property",
    "step": null,
    "startTime": 0,
    "pingTime": 0,
    "progressMessage": null,
    "progressNum": 0,
    "progressTotal": 0,
    "running": false
  },
  "steps": []
}
```

## Run a Migration

```
POST /management/migration/MIGRATION_ID/run
```

### Path Parameters

| Parameter Name   | Type       | Description      |
| ---------------- | ---------- | ---------------- |
| **MIGRATION_ID** | **string** | The migration id.|

### Response

If successful, probes the current state of a migration by analyzing persistent data, sets it as the new current state, then runs the migration asynchronously.

### Status Codes

- 202 _Accepted_ - Success.
- 400 _Bad Request_ - Migration with the given `MIGRATION_ID` does not exist.

### Sample

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/migration/trash-storage/run
```

## Run a Migration Step

```
POST /management/migration/MIGRATION_ID/run/MIGRATION_STEP_ID
```

### Path Parameters

| Parameter Name        | Type       | Description           |
| --------------------- | ---------- | --------------------- |
| **MIGRATION_ID**      | **string** | The migration id.     |
| **MIGRATION_STEP_ID** | **string** | The migration step id.|

### Response

If successful, runs the migration step asynchronously.

### Status Codes

- 202 _Accepted_ - Success.
- 400 _Bad Request_ - Migration with the given `MIGRATION_ID` or `MIGRATION_STEP_ID` does not exist.

### Sample

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/migration/comment-storage/run/property-to-secured
```
