---
title: Connect Endpoint
review:
  comment: ''
  date: '2025-07-15'
  status: ok
labels:
  - http
  - rest-api
  - connect
toc: true
tree_item_index: 600
---

## Get a Nuxeo Connect registration status

```
GET /management/connect/status
```

### Query Parameters

| Parameter Name   | Type        | Description                                     | Notes                          |
| ---------------- | ----------- | ----------------------------------------------- | ------------------------------ |
| **forceRefresh** | **boolean** | Refresh registration status from Connect server | Optional, default is false     |

### Response

If successful, returns a JSON representation of the Connect registration status.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/connect/status
```

```json
{
   "CLID" : "xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx",
   "CTID" : "yyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyyy",
   "contractStatus" : "ok",
   "description" : "",
   "endDate" : "08/11/2027",
   "entity-type" : "connectStatus",
   "instanceType" : "dev",
   "message" : null,
   "registered" : true,
   "registrationExpiration" : "2027-11-08T23:59:00Z"
}
```
