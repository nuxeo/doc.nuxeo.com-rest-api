---
title: Probes Endpoint
review:
  comment: ''
  date: '2021-10-26'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 600
---

## Get All Probes Information

```
GET /management/probes
```

### Response

If successful, returns a JSON representation of all probes information.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/probes
```

```json
{
  "entity-type": "probes",
  "entries": [
    {
      "name": "ldapDirectories",
      "status": {
        "neverExecuted": true,
        "success": false,
        "infos": {
          "info": "[unavailable]"
        }
      },
      "history": {
        "lastRun": null,
        "lastSuccess": "1970-01-01T00:00:00",
        "lastFail": "1970-01-01T00:00:00"
      },
      "counts": {
        "run": 0,
        "success": 0,
        "failure": 0
      },
      "time": 0
    },

    ...other happy probes...

  ]
}
```

## Get Probe Information

```
GET /management/probes/PROBE_NAME
```

### Path Parameters

| Parameter Name | Type       | Description     | Notes    |
| -------------- | ---------- | --------------- | -------- |
| **PROBE_NAME** | **string** | The probe name. | Optional |

If no `PROBE_NAME` is passed, return all probes information, see [Get All Probes Information](#get-all-probes-information).

### Response

If successful, returns a JSON representation of the requested probe information.

### Status Codes

- 200 _OK_ - Success.
- 404 _Not Found_ - Probe with the given `PROBE_NAME` does not exist.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/probes/ldapDirectories
```

```json
{
  "name": "ldapDirectories",
  "status": {
    "neverExecuted": true,
    "success": false,
    "infos": {
      "info": "[unavailable]"
    }
  },
  "history": {
    "lastRun": null,
    "lastSuccess": "1970-01-01T00:00:00",
    "lastFail": "1970-01-01T00:00:00"
  },
  "counts": {
    "run": 0,
    "success": 0,
    "failure": 0
  },
  "time": 0
}
```

## Run a Probe

```
POST /management/probes/PROBE_NAME
```

### Path Parameters

| Parameter Name | Type       | Description     |
| -------------- | ---------- | --------------- |
| **PROBE_NAME** | **string** | The probe name. |

### Response

If successful, returns a JSON representation of the run probe information.

### Status Codes

- 200 _OK_ - Success.
- 404 _Not Found_ - Probe with the given `PROBE_NAME` does not exist.

### Sample

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/probes/ldapDirectories
```

```json
{
  "name": "ldapDirectories",
  "status": {
    "neverExecuted": false,
    "success": true,
    "infos": {
      "info": "No configured LDAP directory"
    }
  },
  "history": {
    "lastRun": "2019-10-31T16:45:49.514",
    "lastSuccess": "2019-10-31T16:45:49.514",
    "lastFail": "1970-01-01T00:00:00"
  },
  "counts": {
    "run": 1,
    "success": 1,
    "failure": 0
  },
  "time": 1
}
```
