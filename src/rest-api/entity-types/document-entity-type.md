---
title: Document Entity Type
review:
    comment: ''
    date: '2019-03-07'
    status: ok
labels:
    - rest-api
toc: true
tree_item_index: 100
---

Representation of a Document.

## Resource Representation

```json
{
  "entity-type": "document",
  "repository": string,
  "uid": string,
  "path": string,
  "type": string,
  "state": string,
  "parentRef": string,
  "isCheckedOut": boolean,
  "isVersion": boolean,
  "isProxy": boolean,
  "proxyTargetId": string,
  "versionableId": string,
  "changeToken": string,
  "isTrashed": boolean,
  "title": string,
  "versionLabel": string,
  "lockOwner": string,
  "lockCreated": string,
  "lastModified": datetime,
  "properties": {
    (key): string,
  },
  "facets": [
    string
  ],
  "contextParameters": {
    (key): string,
  },
}
```

| Property Name               | Value        | Description                                                                             |
| --------------------------- | ------------ | --------------------------------------------------------------------------------------- |
| **entity-type**             | **string**   | The entity type name. Value: the fixed string value `document`.                         |
| **repository**              | **string**   | The document repository name.                                                           |
| **uid**                     | **string**   | The document id.                                                                        |
| **path**                    | **string**   | The document path.                                                                      |
| **type**                    | **string**   | The document type.                                                                      |
| **state**                   | **string**   | The document life cyle state.                                                           |
| **parentRef**               | **string**   | The document parent id.                                                                 |
| **isCheckedOut**            | **boolean**  | Wheter the document is checked out.                                                     |
| **isVersion**               | **boolean**  | Whether the document is a version.                                                      |
| **isProxy**                 | **boolean**  | Whether the document is a proxy.                                                        |
| **proxyTargetId**           | **string**   | **Optional** The proxy source document id.                                              |
| **versionableId**           | **string**   | **Optional** The version series id for the document.                                    |
| **changeToken**             | **string**   | The document current change token.                                                      |
| **isTrashed**               | **boolean**  | Whether the document is trashed.                                                        |
| **title**                   | **string**   | The document title.                                                                     |
| **versionLabel**            | **string**   | **Optional** The document version label.                                                |
| **lockOwner**               | **string**   | **Optional** The lock owner.                                                            |
| **lockCreated**             | **datetime** | **Optional** The lock creation date.                                                    |
| **lastModified**            | **datetime** | The last modification date of the document, uses `dc:modified`.                         |
| **properties**              | **object**   | **Optional** A collection of key-value pairs of properties.                             |
| **properties.(key)**        | **string**   | The property XPath.                                                                     |
| **facets**                  | **list**     | The document facets.                                                                    |
| **contextParameters**       | **object**   | **Optional** A collection of enricher name and value pairs filled by enabled enrichers. |
| **contextParameters.(key)** | **string**   | The enricher name.                                                                      |



**Example**

```bash
curl -u Administrator:Administrator "https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain/workspaces/Sample%20Content/PDF%20and%20Office%20Documents/Sample%20PDF%20File.pdf?fetch-document=versionLabel,lock&enrichers-document=thumbnail&properties=dublincore"
```

```json
{
  "entity-type": "document",
  "repository": "default",
  "uid": "83a8c7f7-7623-4a3f-97a4-c336481e97ab",
  "path": "/default-domain/workspaces/Sample Content/PDF and Office Documents/Sample PDF File.pdf",
  "type": "File",
  "state": "project",
  "parentRef": "de72f8e6-348e-477b-8824-9b1c157b4f7d",
  "isCheckedOut": true,
  "isVersion": false,
  "isProxy": false,
  "changeToken": "1-0",
  "isTrashed": false,
  "title": "Sample PDF File.pdf",
  "versionLabel": "0.0",
  "lockOwner": "Administrator",
  "lockCreated": "2019-03-07T15:19:35.209Z",
  "lastModified": "2018-02-21T21:10:20.757Z",
  "properties": {
    "dc:description": null,
    "dc:language": null,
    "dc:coverage": null,
    "dc:valid": null,
    "dc:creator": "Administrator",
    "dc:modified": "2018-02-21T21:10:20.757Z",
    "dc:lastContributor": "Administrator",
    "dc:rights": null,
    "dc:expired": null,
    "dc:format": null,
    "dc:created": "2018-02-21T21:10:20.757Z",
    "dc:title": "Sample PDF File.pdf",
    "dc:issued": null,
    "dc:nature": null,
    "dc:subjects": [],
    "dc:contributors": ["Administrator"],
    "dc:source": null,
    "dc:publisher": null
  },
  "facets": ["Versionable", "NXTag", "Publishable", "Commentable", "HasRelatedText", "Thumbnail", "Downloadable"],
  "contextParameters": {
    "thumbnail": {
      "url": "https://nightly.nuxeo.com/nuxeo/api/v1/repo/default/id/83a8c7f7-7623-4a3f-97a4-c336481e97ab/@rendition/thumbnail?changeToken=1-0"
    }
  }
}
```

## Enrichers

### acls

Get the document ACLs.

See [ACLJsonEnricher](http://community.nuxeo.com/api/nuxeo/latest/javadoc/org/nuxeo/ecm/permissions/ACLJsonEnricher.html) for more details.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: acl" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "acls": [{
      "name": "local",
      "aces": [{
        "username": "jsmith",
        "permission": "ReadWrite",
        "granted": true
      }]
    }, {
      "name": "inherited",
      "aces": [{
        "username": "jdoe",
        "permission": "Everything",
        "granted": true
      }, {
        "username": "Administrator",
        "permission": "Everything",
        "granted": true
      }, {
        "username": "members",
        "permission": "Read",
        "granted": true
      }]
    }]
  }
}
```

### audit

Get the document latest log entries.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: audit" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "audit": [{
      "entity-type": "logEntry",
      "id": 438,
      "category": "eventDocumentCategory",
      "principalName": "Administrator",
      "comment": null,
      "docLifeCycle": "project",
      "docPath": "/default-domain/workspaces/Sample Content/PDF and Office Documents/Sample PDF File.pdf",
      "docType": "File",
      "docUUID": "83a8c7f7-7623-4a3f-97a4-c336481e97ab",
      "eventId": "documentLocked",
      "repositoryId": "default",
      "eventDate": "2019-03-07T15:19:35.210Z",
      "logDate": "2019-03-07T15:19:35.630Z",
      "extended": {}
    }]
  }
}
```

### breadcrumb

Get the list of all parent documents.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: breadcrumb" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "breadcrumb": {
      "entity-type": "documents",
      "entries": [{
        "entity-type": "document",
        "path": "/default-domain",
        "type": "Domain",
        "state": "project",
        "parentRef": "00000000-0000-0000-0000-000000000000",
        "isCheckedOut": true,
        "isVersion": false,
        "isProxy": false,
        "changeToken": "2-0",
        "isTrashed": false,
        "title": "Domain",
        "lastModified": "2019-03-07T11:56:50.577Z",
        "facets": ["Folderish", "NXTag", "SuperSpace", "NotCollectionMember"]
      }, {
        "entity-type": "document",
        "repository": "default",
        "uid": "f489ecc9-cc5b-4fbd-ad63-aa7c693e1b8e",
        "path": "/default-domain/workspaces",
        "type": "WorkspaceRoot",
        "state": "project",
        "parentRef": "442b27de-0331-41b1-bdfd-0f9dbc391a18",
        "isCheckedOut": true,
        "isVersion": false,
        "isProxy": false,
        "changeToken": "3-0",
        "isTrashed": false,
        "title": "Workspaces",
        "lastModified": "2019-03-07T11:56:51.314Z",
        "facets": ["Folderish", "NXTag", "SuperSpace", "HiddenInCreation", "NotCollectionMember"]
      }]
    }
  }
}
```

### children

Get the list of all children documents.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: children" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "children": {
      "entity-type": "documents",
      "entries": [{
        "entity-type": "document",
        "repository": "default",
        "uid": "f489ecc9-cc5b-4fbd-ad63-aa7c693e1b8e",
        "path": "/default-domain/workspaces",
        "type": "WorkspaceRoot",
        "state": "project",
        "parentRef": "442b27de-0331-41b1-bdfd-0f9dbc391a18",
        "isCheckedOut": true,
        "isVersion": false,
        "isProxy": false,
        "changeToken": "3-0",
        "isTrashed": false,
        "title": "Workspaces",
        "lastModified": "2019-03-07T11:56:51.314Z",
        "facets": ["Folderish", "NXTag", "SuperSpace", "HiddenInCreation", "NotCollectionMember"]
      }, {
        "entity-type": "document",
        "repository": "default",
        "uid": "a878eb77-a19e-4fc3-b8a4-68ec8094ed13",
        "path": "/default-domain/sections",
        "type": "SectionRoot",
        "state": "project",
        "parentRef": "442b27de-0331-41b1-bdfd-0f9dbc391a18",
        "isCheckedOut": true,
        "isVersion": false,
        "isProxy": false,
        "changeToken": "2-0",
        "isTrashed": false,
        "title": "Sections",
        "lastModified": "2019-03-07T11:56:50.587Z",
        "facets": ["Folderish", "NXTag", "SuperSpace", "HiddenInCreation", "NotCollectionMember", "MasterPublishSpace"]
      }]
    }
  }
}
```

### collections

Get the collections the document belongs to.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: collections" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "collections": [{
      "changeToken": "1464771452017",
      "entity-type": "document",
      "facets": [
        "Versionable",
        "Collection",
        "NotCollectionMember"
      ],
      "isCheckedOut": true,
      "lastModified": "2016-06-01T08:57:32.01Z",
      "parentRef": "8e62af0a-a74c-4bd1-96a4-66034834bf3b",
      "path": "/default-domain/UserWorkspaces/Administrator/Collections/Fox Icons",
      "repository": "default",
      "state": "project",
      "title": "Fox Icons",
      "type": "Collection",
      "uid": "50110ba5-b129-40b2-9880-3d9783710404"
    }]
  }
}
```

### contextualParameters???

### documentURL

Get the document URL.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: documentURL" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "documentURL": "https://NUXEO_SERVER/nuxeo/ui/#!/doc/DOC_ID"
}
```

### driveEditURL

Get the document drive edit URL.

**Example**

```bash
curl -u USERNAME:PASSWORD -H "enrichers-document: driveEditURL" https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
```

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "documentURL": "https://NUXEO_SERVER/nuxeo/ui/#!/doc/DOC_ID"
}
```

### favorites
### firstAccessibleAncestor
### hasContent
### hasFolderishChild
### highlight
### pendingTasks
### permissions
### preview
### publications
### renditions
### runnableWorkflows
### runningWorkflows
### subscribedNotifications
### subtypes
### tags
### thumbnail
### userVisiblePermissions
### vocabularies?????

### Bar

## Fetch Properties