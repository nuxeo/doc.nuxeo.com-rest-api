---
title: Authentication
review:
    comment: ''
    date: '2019-07-24'
    status: ok
labels:
    - authentication
toc: true
tree_item_index: 100
---

The request authentication depends on the configured authentication chain. The [default authentication chain](http://explorer.nuxeo.com/nuxeo/site/distribution/latest/viewContribution/org.nuxeo.ecm.restapi.server.auth.config--specificChains) for the REST API includes:
- Basic
- Token
- JWT
- Bearer Token

## Basic Authentication

Authenticate with Base64-encoded credentials:

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Authorization: Basic BASE_64_CREDENTIALS
```

## Token Authentication

Authenticate with a Nuxeo login token:

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
X-Authentication-Token: NUXEO_TOKEN
```

## JWT Authentication

Authenticate with a JWT token:

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Authorization: Bearer JWT_TOKEN
```

## OAuth 2.0 Access Token Authentication

Authenticate with an OAuth 2.0 access token:

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
Authorization: Bearer OAUTH2_TOKEN
```

* * *

<div class="row" data-equalizer data-equalize-on="medium">
<div class="column medium-6">

{{#> panel heading='Related Documentation'}}

- [Authentication and User Management]({{page page='authentication-and-user-management'}})
- [OAuth 2.0]({{page page='using-oauth2'}})

{{/panel}}

</div>
<div class="column medium-6">

&nbsp;

</div>
</div>
