---
title: Task Fetch Properties
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

## workflowInitiator

Fetch the `workflowInitiator` task property as a [User entity]({{page page='user-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/task/TASK_ID
fetch.task: workflowInitiator
```
---

## targetDocumentIds

Fetch the `targetDocumentIds` task property as a list of [Document entity]({{page page='document-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/task/TASK_ID
fetch.task: targetDocumentIds
```
---

## actors

Fetch the `actors` and `delegatedActors` task properties as lists of [User entity]({{page page='user-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/task/TASK_ID
fetch.task: actors
```
---
