---
title: Configuration Endpoint
review:
  comment: ''
  date: '2023-07-17'
  status: ok
labels:
  - http
  - rest-api
  - configuration
toc: true
tree_item_index: 600
---

## Get a Nuxeo instance's configuration

```
GET /management/configuration
```

### Response

If successful, returns a JSON representation of all configured properties and all runtime properties with sensitive informations redacted.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u <user>:<password> <nuxeoHost>:8080/nuxeo/api/v1/management/configuration
```

```json
{
  "configuredProperties": {
    "NUXEO_HOME": "...",
    ...
  }
  "runtimeProperties": {
    "NUXEO_HOME": "...",
    ...
  }
}
```
