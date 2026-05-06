---
title: Management Endpoint
review:
  comment: ''
  date: '2021-10-22'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 800
---

The Nuxeo Management REST API is a set of endpoints allowing the management of the Nuxeo Platform.

## Configuration

### Authentication

The Management REST API is accessible for any administrator user.

Furthermore, a "technical" user can be configured to access the Management REST API in `nuxeo.conf`:

```
nuxeo.management.api.user=transient/technical_user
```

The user does not need to exist in Nuxeo, and **must** start with `transient/` as we are relying on the transient user feature.

{{#> callout type='info' heading='Since 2025.16'}}
Every call made to the Management REST API fires a `managementApiAccess` event. By contributing an Audit [route]({{page version='' space='nxdoc' page='audit-router'}}) and the appropriate [extended info]({{page version='' space='nxdoc' page='audit'}}#extendedinfo) mappings on this event, you can persist who called what, when and how to the [Audit]({{page version='' space='nxdoc' page='audit'}}) service to enable full traceability of the Management REST API. See the [worked example]({{page version='' space='nxdoc' page='audit-router'}}#worked-example-routing-a-business-event-to-a-secondary-backend) on the Audit Router page.
{{/callout}}

Once you have created the user, configure a JWT secret in `nuxeo.conf`:

```
nuxeo.jwt.secret=abracadabra
```

Then, to use the Management REST API:

- Share the JWT secret (`abracadabra` here) between the Nuxeo Server and the client calling the Management REST API,
- Generate a JWT token with the user (`transient/technical_user` here) as claim subject,
- Call the API using the `Authorization: Bearer JWT_TOKEN` header.

### Deploy the Management REST API on a Separate HTTP Port

For security reasons, it is recommended to deploy the Management REST API on a different port from the regular Nuxeo application one.

For instance, to configure the HTTP port to `9090`, in `nuxeo.conf` add:

```
nuxeo.management.api.http.port=9090
```

## Endpoints

Here are the endpoints provided by the Management REST API.

| Name                                                       | Endpoint             | Description                    |
|------------------------------------------------------------|----------------------|--------------------------------|
| [Audit]({{page page='audit-endpoint'}})                    | **/audit**           | Audit Router introspection and Blue/Green Audit migration. |
| [Binaries]({{page page='binaries-endpoint'}})              | **/binaries**        | Binaries management.           |
| [Blobs]({{page page='blobs-endpoint'}})                    | **/blobs**           | Blobs management.              |
| [Bulk]({{page page='bulk-endpoint'}})                      | **/bulk**            | Bulk actions management.       |
| [Configuration]({{page page='configuration-endpoint'}})    | **/configuration**   | Configuration information.     |
| [Connect]({{page page='connect-endpoint'}})                | **/connect**         | Connect information.           |
| [Distribution]({{page page='distribution-endpoint'}})      | **/distribution**    | Distribution information.      |
| [Elasticsearch]({{page page='elasticsearch-endpoint'}})    | **/elasticsearch**   | Elasticsearch management.      |
| [Fulltext]({{page page='fulltext-endpoint'}})              | **/fulltext**        | Fulltext management.           |
| [Migration]({{page page='migration-endpoint'}})            | **/migration**       | Migrations management.         |
| [OAuth2]({{page page='oauth2-endpoint'}})                  | **/oauth2**          | OAuth2 management.             |
| [PageProviders]({{page page='page-providers-endpoint'}})   | **/page-providers**  | Page Providers information.    |
| [Pictures]({{page page='pictures-endpoint'}})              | **/pictures**        | Picture views recomputation.   |
| [Probes]({{page page='probes-endpoint'}})                  | **/probes**          | Probes information.            |
| [Scheduler]({{page page='scheduler-endpoint'}})            | **/scheduler**       | Scheduler Management.          |
| [Search]({{page page='stearch-endpoint'}})                 | **/search**          | Nuxeo Search Management.       |
| [Streams]({{page page='stream-endpoint'}})                 | **/stream**          | Nuxeo Stream Management.       |
| [Thumbnails]({{page page='thumbnails-endpoint'}})          | **/thumbnails**      | Thumbnails recomputation.      |
| [Versions]({{page page='versions-endpoint'}})              | **/versions**        | Versions management.           |
| [Workflows]({{page page='workflows-endpoint'}})            | **/workflows**       | Workflows management.          |
| [WorkManager]({{page page='workmanager-endpoint'}})        | **/work-manager**    | Works in failure reprocessing. |
