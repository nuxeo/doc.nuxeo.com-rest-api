---
title: Page Providers Endpoint
review:
    comment: ''
    date: '2023-02-14'
    status: ok
labels:
    - http
    - rest-api
toc: true
tree_item_index: 500
---

## List Page Providers

```
GET /management/page-providers
```

### Response

Returns a list of all registered Page Providers.

### Status Codes**

- 200 *OK* - Success.

### Sample

```curl
curl -X GET -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/page-providers
```

```json
[
  {
    "name": "GET_DOCUMENTS_FOR_TAG_AND_USER",
    "class": "org.nuxeo.ecm.platform.query.nxql.CoreQueryAndFetchPageProvider",
    "maxPageSize": 0
  },
  {
    "name": "nxql_search",
    "class": "org.nuxeo.ecm.platform.query.nxql.CoreQueryDocumentPageProvider",
    "maxPageSize": 1000
  },
  ...
  {
    "name": "expired_search",
    "class": "org.nuxeo.elasticsearch.provider.ElasticSearchNxqlPageProvider",
    "maxPageSize": 1000
  },
  ...
  {
    "name": "LATEST_AUDITED_CREATED_USERS_OR_GROUPS_PROVIDER",
    "class": "org.nuxeo.elasticsearch.audit.pageprovider.ESDocumentHistoryPageProvider",
    "maxPageSize": 100
  },
  ...
  {
    "name": "users_listing",
    "class": "org.nuxeo.ecm.platform.usermanager.providers.UsersPageProvider",
    "maxPageSize": 1000
  }
]

```

