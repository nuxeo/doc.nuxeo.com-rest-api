---
title: Workflow Fetch Properties
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

## initiator

Fetch the `initiator` task property as a [User entity]({{page page='user-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/workflow/WORKFLOW_ID
fetch.workflow: initiator
```
---

## attachedDocumentIds

Fetch the `attachedDocumentIds` task property as a list of [Document entity]({{page page='document-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/workflow/WORKFLOW_ID
fetch.workflow: attachedDocumentIds
```
---
