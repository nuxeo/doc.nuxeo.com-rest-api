---
title: Distribution Endpoint
review:
    comment: ''
    date: '2021-10-26'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 300
---

## Get the Distribution Information

```
GET /management/distribution
```

### Response

If successful, returns a JSON representation of the distribution information.

### Status Codes

- 200 *OK* - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/distribution
```

```json
{
  "org.nuxeo.ecm.product.name": "Nuxeo Platform",
  "org.nuxeo.ecm.product.version": "LTS 2019-HF17",
  "org.nuxeo.distribution.name": "server",
  "org.nuxeo.distribution.version": "10.10",
  "org.nuxeo.distribution.server": "tomcat",
  "org.nuxeo.distribution.date": "201901211253",
  "warnings": [],
  "nuxeo.osgi.bundles": [
    {
      "name": "org.nuxeo.admin.center",
      "version": "10.10-HF11"
    },

    ...other happy bundles...

  ]
}
```

## Get the List of Installed Packages

```
GET /management/distribution/packages
```

### Response

If successful, returns a JSON representation of the installed packages.

### Status Codes

- 200 *OK* - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/distribution/packages
```

```json
{
  "entity-type": "packages",
  "entries": [
    {
      "entity-type": "package",
      "id": "nuxeo-web-ui-2025.12.0",
      "name": "nuxeo-web-ui",
      "title": "Nuxeo Web UI",
      "description": "Web UI is the primary UI for the Nuxeo Platform. It is an ideal starting point for any Digital Asset Management, Case Management or Document Management project.",
      "version": "2025.12.0",
      "type": "ADDON",
      "state": "STARTED",
      "targetPlatforms": [],
      "vendor": "Nuxeo",
      "supportsHotReload": false,
      "provides": [],
      "dependencies": [],
      "conflicts": [],
      "licenseType": "Apache License, Version 2.0",
      "licenseUrl": "http://www.apache.org/licenses/LICENSE-2.0.html"
    },

    ...other happy packages...
  ]
}
```
