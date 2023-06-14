---
title: Endpoints
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - http
    - rest-api
tree_item_index: 400
---

Here are the endpoints provided by the Nuxeo REST API.

| Name                                                    | Endpoint          | Description                                                      |
| ------------------------------------------------------- | ----------------- | ---------------------------------------------------------------- |
| [Automation]({{page page='automation-endpoint'}})       | **/automation**   | Call an operation or chain of operations deployed on the server. |
| Batch Upload                                            | **/upload**       | Upload a set of files to use them in a transactional operation.  |
| [Capabilities]({{page page='capabilities-endpoint'}})   | **/capabilities** | Get the server capabilities.                                     |
| [Data Model]({{page page='data-model-endpoint'}})       | **/config**       | Introspection of the facets, schemas and document types.         |
| [Directory]({{page page='directory-endpoint'}})         | **/directory**    | CRUD on directories.                                             |
| [Document Id]({{page page='document-id-endpoint'}})     | **/id**           | CRUD on documents by id.                                         |
| [Document Path]({{page page='document-path-endpoint'}}) | **/path**         | CRUD on documents by path.                                       |
| [Group]({{page page='group-endpoint'}})                 | **/group**        | CRUD on groups.                                                  |
| [Management]({{page page='management-endpoint'}})       | **/management**   | Management REST API.                                             |
| [OAuth 2.0]({{page page='oauth2-endpoints'}})           | **/oauth2**       | CRUD on OAuth 2.0 clients, providers and tokens.                 |
| [Search]({{page page='search-endpoints'}})              | **/search**       | Perform searches by query or page provider and save searches.    |
| [Task]({{page page='task-endpoint'}})                   | **/task**         | Handle tasks.                                                    |
| [User]({{page page='user-endpoint'}})                   | **/user**         | CRUD on users.                                                   |
| Workflow                                                | **/workflow**     | Handle workflows.                                                |

## Learn More

- Test the Nuxeo REST API endpoints on your local instance with the [Nuxeo API Playground](http://nuxeo.github.io/api-playground/), see [documentation]({{page space='nxdoc' page='nuxeo-api-playground'}}).
- Check out the Nuxeo REST API explorer of your instance at https://NUXEO_SERVER/nuxeo/api/v1/doc.
- Learn how to [Contribute a REST API Endpoint]({{page page='how-to-contribute-to-the-rest-api'}}#contributing-a-rest-api-endpoint).
