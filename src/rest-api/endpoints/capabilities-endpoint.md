---
title: Capabilities
review:
    comment: ''
    date: '2023-06-13'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 250
---


## Get a Bulk Action Status

```
GET /capabilities
```

### Response

If successful, returns a [capabilities entity]({{page page='capabilities-entity-type'}}) representing the capabilities of the server.

### Status Codes

- 200 *OK* - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/capabilities
```

```json
{
  "entity-type" : "capabilities",
  "cluster" : {
    "enabled" : false,
    "nodeId" : "347729645706513753"
  },
  "repository" : {
    "default" : {
        "queryBlobKeys" : false
    }
  },
  "server" : {
    "distributionName" : "lts",
    "distributionServer" : "tomcat",
    "distributionVersion" : "2021.39.3"
  }
}
```
