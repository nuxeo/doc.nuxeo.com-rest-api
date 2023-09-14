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

If successful, returns a JSON representation of configured properties (the ones from the configuration.properties file) and the runtime properties (the ones from Framework#getProperties) with sensitive informations redacted.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/configuration
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
