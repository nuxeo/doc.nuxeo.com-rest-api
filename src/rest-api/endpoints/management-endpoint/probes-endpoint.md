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
tree_item_index: 500
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

## Run all Probes

```
POST /management/probes
```

### Response

If successful, returns a JSON representation of the run probes information.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/probes
```

```json
{
   "entity-type" : "probes",
   "entries" : [
      {
         "counts" : {
            "failure" : 0,
            "run" : 1,
            "success" : 1
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.148Z",
            "lastSuccess" : "2025-07-15T13:33:19.148Z"
         },
         "name" : "remoteSQLStorageSessions",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "info" : "Actives remote session for SQL repositories:<br /><b>default</b><br/>"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 1
      },
      {
         "counts" : {
            "failure" : 0,
            "run" : 1,
            "success" : 1
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.149Z",
            "lastSuccess" : "2025-07-15T13:33:19.149Z"
         },
         "name" : "runtimeStatus",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "info" : "Runtime started"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 0
      },
      {
         "counts" : {
            "failure" : 0,
            "run" : 1,
            "success" : 1
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.149Z",
            "lastSuccess" : "2025-07-15T13:33:19.149Z"
         },
         "name" : "activeRepositorySessions",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "info" : "Actives sessions for SQL repositories:<br /><b>default</b>: 0<br />"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 0
      },
      {
         "counts" : {
            "failure" : 0,
            "run" : 1,
            "success" : 1
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.149Z",
            "lastSuccess" : "2025-07-15T13:33:19.149Z"
         },
         "name" : "administrativeStatus",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "host" : "localhost",
               "server" : "Linux-24d0eaad33f333aa5781124fccfb97f7-76b5d3908b7a402fa96850e21d99ae1f",
               "status" : "active"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 4
      },
      {
         "counts" : {
            "failure" : 0,
            "run" : 1,
            "success" : 1
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.153Z",
            "lastSuccess" : "2025-07-15T13:33:19.153Z"
         },
         "name" : "repositoryStatus",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "info" : "Repository started"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 2
      },
      {
         "counts" : {
            "failure" : 0,
            "run" : 1,
            "success" : 1
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.155Z",
            "lastSuccess" : "2025-07-15T13:33:19.155Z"
         },
         "name" : "streamStatus",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "info" : "No failure"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 0
      },
      {
         "counts" : {
            "failure" : 0,
            "run" : 2,
            "success" : 2
         },
         "entity-type" : "probe",
         "history" : {
            "lastFail" : "1970-01-01T00:00:00.000Z",
            "lastRun" : "2025-07-15T13:33:19.155Z",
            "lastSuccess" : "2025-07-15T13:33:19.155Z"
         },
         "name" : "ldapDirectories",
         "status" : {
            "entity-type" : "probeStatus",
            "infos" : {
               "info" : "No configured LDAP directory"
            },
            "neverExecuted" : false,
            "success" : true
         },
         "time" : 0
      }
   ]
}
```
