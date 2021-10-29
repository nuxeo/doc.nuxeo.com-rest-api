---
title: Document Fetch Properties
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

Fetch properties on a [Document entity]({{page page='document-entity-type'}}) are used to load values referenced by the properties. The fetch property name is the property xpath, such as `dc:creator`.

## properties

Fetch all referenced values.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: properties
```
---

## dc:creator

Fetch the `dc:creator` document property as a [User entity]({{page page='user-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:creator
```
---

## dc:lastContributor

Fetch the `dc:lastContributor` document property as a [User entity]({{page page='user-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:lastContributor
```
---

## dc:contributors

Fetch the `dc:contributors` document property as a list of [User entity]({{page page='user-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:contributors
```
---

## dc:subjects

Fetch the `dc:subjects` document property as a list of [Directory Entry entity]({{page page='directory-entry-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:subjects
```
---

## dc:coverage

Fetch the `dc:coverage` document property as a list of [Directory Entry entity]({{page page='directory-entry-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:coverage
```
---

## dc:nature

Fetch the `dc:nature` document property as a [Directory Entry entity]({{page page='directory-entry-entity-type'}}#resource-representation).

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
fetch.document: dc:nature
```
---
