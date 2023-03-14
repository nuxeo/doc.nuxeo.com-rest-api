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
org.nuxeo.rest.management.user=transient/technical_user
```

The user does not need to exist in Nuxeo, and **must** start with `transient/` as we are relying on the transient user feature.

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
nuxeo.server.http.managementPort=9090
```

## Endpoints

Here are the endpoints provided by the Management REST API.

| Name                                                       | Endpoint             | Description                    |
|------------------------------------------------------------|----------------------|--------------------------------|
| [Binaries]({{page page='binaries-endpoint'}})              | **/binaries**        | Binaries management.           |
| [Bulk]({{page page='bulk-endpoint'}})                      | **/bulk**            | Bulk actions management.       |
| [Distribution]({{page page='distribution-endpoint'}})      | **/distribution**    | Distribution information.      |
| [Elasticsearch]({{page page='elasticsearch-endpoint'}})    | **/elasticsearch**   | Elasticsearch management.      |
| [Fulltext]({{page page='fulltext-endpoint'}})              | **/fulltext**        | Fulltext management.           |
| [PageProviders]({{page page='page-providers-endpoint'}})   | **/page-providers**  | Page Providers information.    |
| [Pictures]({{page page='pictures-endpoint'}})              | **/pictures**        | Picture views recomputation.   |
| [Probes]({{page page='probes-endpoint'}})                  | **/probes**          | Probes information.            |
| [Streams]({{page page='stream-endpoint'}})                 | **/stream**          | Nuxeo Stream Management.       |
| [Thumbnails]({{page page='thumbnails-endpoint'}})          | **/thumbnails**      | Thumbnails recomputation.      |
| [Versions]({{page page='versions-endpoint'}})              | **/versions**        | Versions management.           |
| [Workflows]({{page page='workflows-endpoint'}})            | **/workflows**       | Workflows management.          |
| [WorkManager]({{page page='workmanager-endpoint'}})        | **/work-manager**    | Works in failure reprocessing. |
