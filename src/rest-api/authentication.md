---
title: Authentication
review:
    comment: ''
    date: '2019-03-06'
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

Authenticate with a `username` and `password`:

```bash
curl -u USERNAME:PASSWORD  https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain
```

Authenticate with the `Authorization` header:

```bash
curl -H "Authorization: Basic QWRtaW5pc3RyYXRvcjpBZG1pbmlzdHJhdG9y" https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain
```

## Token Authentication

Authenticate with a Nuxeo login token:

```bash
curl -H "X-Authentication-Token: NUXEO_TOKEN" https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain
```

## JWT Authentication

Authenticate with a JWT token:

```bash
curl -H "Authorization: Bearer JWT_TOKEN" https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain
```

## OAuth 2.0 Access Token Authentication

Authenticate with an OAuth 2.0 access token:

```bash
curl -H "Authorization: Bearer OAUTH2_TOKEN" https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain
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