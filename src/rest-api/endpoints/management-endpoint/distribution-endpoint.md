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
