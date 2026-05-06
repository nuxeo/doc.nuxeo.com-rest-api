---
title: Audit Endpoint
review:
  comment: ''
  date: '2026-05-06'
  status: ok
labels:
  - http
  - rest-api
  - audit
toc: true
---

{{#> callout type='warning' heading='Only available since 2025.19'}}
This endpoint has been introduced in Nuxeo 2025.19 along with the new contributable [Audit Router]({{page version='' space='nxdoc' page='audit-router'}}) and the support of multiple Audit Backends (Blue/Green Audit migration).
{{/callout}}

The Audit endpoint exposes operations to operate a Blue/Green Audit migration (copy and verification) between two Audit Backends, and to introspect the live audit routing topology.

## Copy an Audit Backend to Another

```
POST /management/audit/copy
```

Triggers a [bulk action]({{page page='bulk-endpoint'}}) (`copyAudit`) that scrolls the source Audit Backend and writes every `LogEntry` to the target Audit Backend. This is the primary operation used to perform a Blue/Green Audit migration, for instance when upgrading from an OpenSearch 1.x to an OpenSearch 2.x cluster, or from MongoDB to OpenSearch.

The bulk action runs as the `system` user and is exclusive: a second `/copy` call between the same backends will be rejected as long as the previous one is not finished.

### Form Parameters

| Parameter Name | Type       | Description                                          | Notes    |
|----------------|------------|------------------------------------------------------|----------|
| **from**       | **string** | The name of the source Audit Backend to copy from.   | Required |
| **to**         | **string** | The name of the target Audit Backend to copy to.     | Required |

### Response

If successful, returns a [bulk status entity]({{page page='bulk-status-entity-type'}}) representing the bulk action status of the `copyAudit` action.

The copy progress can then be monitored using the [Bulk Endpoint]({{page page='bulk-endpoint'}}).

### Status Codes

- 200 _OK_ - Success.
- 400 _Bad Request_ - `from` or `to` is missing or blank.
- 409 _Conflict_ - A copy is already running.

### Sample

To copy all log entries from the `default` Audit Backend to the `other` Audit Backend:

```curl
curl -X POST -u Administrator:Administrator \
--data-urlencode "from=default" \
--data-urlencode "to=other" \
http://localhost:8080/nuxeo/api/v1/management/audit/copy
```

```json
{
  "entity-type": "bulkStatus",
  "commandId": "0e1e6800-631a-4e04-a47c-241ea7b3596a",
  "state": "SCHEDULED",
  "processed": 0,
  "error": false,
  "errorCount": 0,
  "total": 0,
  "action": "copyAudit",
  "username": "system",
  "submitted": "2026-05-06T14:00:00.000Z",
  "scrollStart": null,
  "scrollEnd": null,
  "processingStart": null,
  "processingEnd": null,
  "completed": null,
  "processingMillis": 0
}
```

## Check the Result of a Copy Across Audit Backends

```
GET /management/audit/checkSearch
```

Runs the same NXQL query against several Audit Backends in parallel and reports the result of each execution. This is used to verify the result of a Blue/Green Audit migration triggered by [`POST /management/audit/copy`](#copy-an-audit-backend-to-another), by comparing the number of `LogEntry`s and the actual log entry identifiers returned by each backend.

### Query Parameters

| Parameter Name | Type       | Description                                                       | Notes                                                                |
|----------------|------------|-------------------------------------------------------------------|----------------------------------------------------------------------|
| **nxql**       | **string** | The NXQL query to execute against each Audit Backend.             | Optional, defaults to `SELECT * FROM LogEntry`                       |
| **pageSize**   | **number** | The number of log entries to return per backend execution.        | Optional                                                             |
| **backend**    | **string** | The name of an Audit Backend to query. Repeat to query several.   | Required, at least one value must be provided.                       |

### Response

If successful, returns a JSON response with one entry per Audit Backend listed in the `backend` query parameter, each containing the execution duration, the total result count, the result count limit and the matching `LogEntry` identifiers.

Note that only log entry identifiers are returned, this is on purpose because the management endpoint should not expose the audit content.

### Status Codes

- 200 _OK_ - Success.
- 400 _Bad Request_ - No `backend` query parameter has been provided.

### Sample

To check that the `default` and `other` Audit Backends contain the same log entries after a copy:

```curl
curl -X GET -u Administrator:Administrator \
--data-urlencode "nxql=SELECT * FROM LogEntry" \
--data-urlencode "pageSize=5" \
--data-urlencode "backend=default" \
--data-urlencode "backend=other" \
-G http://localhost:8080/nuxeo/api/v1/management/audit/checkSearch
```

```json
{
  "pageProvider": "audit_check_nxql",
  "orders": [
    "logDate DESC"
  ],
  "executions": {
    "default": {
      "duration": "324ms",
      "resultsCount": 1234,
      "resultsCountLimit": 0,
      "results": [
        "1",
        "2",
        "3",
        "4",
        "5"
      ]
    },
    "other": {
      "duration": "22ms",
      "resultsCount": 1234,
      "resultsCountLimit": 10000,
      "results": [
        "1",
        "2",
        "3",
        "4",
        "5"
      ]
    }
  }
}
```

If the `resultsCount` differs between the two backends, or if the `results` arrays do not match, further investigation can be done by running the `audit_check_nxql` page provider directly on each backend, for instance:

```curl
curl -X GET -u Administrator:Administrator \
--data-urlencode "queryParams=SELECT * FROM LogEntry" \
--data-urlencode "pageSize=5" \
--data-urlencode "namedParameters={\"backendName\":\"default\"}" \
-G http://localhost:8080/nuxeo/api/v1/search/pp/audit_check_nxql/execute
```

## Get the Audit Router Introspection

```
GET /management/audit/introspection
```

Returns a [PlantUML](https://plantuml.com/) representation of the live audit routing graph, which includes events that are listened to, how the `audit/audit` stream feeds the `audit/writer` computation, and how the [Audit Router]({{page version='' space='nxdoc' page='audit-router'}}) dispatches `LogEntry`s to the contributed Audit Backends.

### Response

A `text/x-plantuml` document describing the audit routing topology.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
-H "Accept: text/x-plantuml" \
http://localhost:8080/nuxeo/api/v1/management/audit/introspection
```

```text
@startuml
title Audit Router Introspection

hide members
...
component event_listener [
Event Listener
----
events:
- documentCreated
- documentModified
- documentRemoved
- ...
]
queue stream_audit_audit as "audit/audit" {
  component computation_audit_writer [
  audit/writer
  ]
}
event_listener==>stream_audit_audit
stream_audit_audit=[hidden]=>stream_audit_audit.computation_audit_writer
package audit_router as "Audit Router" {
  component route_default [
  default
  ]
  component route_other [
  other
  ]
}
package audit_backend as "Audit Backends" {
  database backend_default as "default" {
    class implementation as "OpenSearchAuditBackend" {
    }
  }
  backend_default=[hidden]=>backend_default.implementation
  database backend_other as "other" {
    class implementation as "MemAuditBackend" {
    }
  }
  backend_other=[hidden]=>backend_other.implementation
}
stream_audit_audit.computation_audit_writer==>audit_router
audit_router==>audit_router.route_default
audit_router.route_default==>audit_backend.backend_default
audit_router==>audit_router.route_other
audit_router.route_other==>audit_backend.backend_other
@enduml
```

The PlantUML output can then be turned into a diagram using any PlantUML renderer. The diagram below was generated by submitting the `@startuml ... @enduml` block above to the public [PlantUML server](https://www.plantuml.com/plantuml/) and downloading the resulting PNG.

![Audit Router Introspection]({{file name='audit-router-introspection.png'}} ?border=true)

## Learn More

- [Audit Router]({{page version='' space='nxdoc' page='audit-router'}})
- [Blue/Green Audit Migration]({{page version='' space='nxdoc' page='copy-audit-backend'}})
- [Bulk Endpoint]({{page page='bulk-endpoint'}})
