---
title: Document Enrichers
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: true
---

## acls

Get the document ACLs.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: acls
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "acls": [
      {
        "name": string,
        "aces": [
          {
            "id": string,
            "username": string | <a href="../user-entity-type#resource-representation">User entity</a>,
            "externalUser": boolean,
            "permission": string,
            "granted": boolean,
            "creator": string | <a href="../user-entity-type#resource-representation">User entity</a>,,
            "begin": datetime,
            "end": datetime,
            "status": string,
            "notify": boolean,
            "comment": string
          }
        ]
      }
    ]
  }
}
</code></pre>

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**name**</td>
        <td>**string**</td>
        <td>The ACL name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[]**</td>
        <td>**list**</td>
        <td>The list of the ACEs (Access Control Entry).</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].id**</td>
        <td>**string**</td>
        <td>The ACE id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].username**</td>
        <td>**string** <br /> or **object**</td>
        <td>
          The ACE username.<br />
          Or the ACE username user entity, if the fetch property `username` is set.
        </td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].externalUser**</td>
        <td>**string**</td>
        <td>The ACL name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].permission**</td>
        <td>**string**</td>
        <td>The ACE permission.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].granted**</td>
        <td>**boolean**</td>
        <td>Whether the ACE is granted.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].creator**</td>
        <td>**string** <br /> or **object**</td>
        <td>
          The ACE creator.<br />
          Or the ACE creator user entity, if the fetch property `creator` is set.
        </td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].begin**</td>
        <td>**datetime**</td>
        <td>The ACE begin date (W3C date-time).</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].end**</td>
        <td>**datetime**</td>
        <td>The ACE end date (W3C date-time).</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].status**</td>
        <td>**string**</td>
        <td>The ACE status. Value: `pending`, `effective` or `archived`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aces[].notify**</td>
        <td>**boolean**</td>
        <td>Whether to notify the user when the ACE becomes effective.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**aces[].comment**</td>
        <td>**string**</td>
        <td>The comment for the user when the ACE becomes effective.</td>
        <td>Optional</td>
      </tr>
    </tbody>
  </table>
</div>

---

## audit

Get the document latest log entries.

### Invokation

```bash
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: audit
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "audit": [
      <a href="../log-entry-entity-type#resource-representation">Log Entry entity</a>,
    ]
  }
}
</code></pre>

---

## breadcrumb

Get the list of all parent documents.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: breadcrumb
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "breadcrumb": {
      "entity-type": "documents",
      "entries": [
        <a href="../document-entity-type#resource-representation">Document entity</a>
      ]
    }
  }
}
</code></pre>

---

## children

Get the list of all children documents.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: children
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  "path": "/default-domain",
  ...
  "contextParameters": {
    "children": {
      "entity-type": "documents",
      "entries": [
        <a href="../document-entity-type#resource-representation">Document entity</a>
      ]
    }
  }
}
</code></pre>

---

## collections

Get the collections the document belongs to.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: collections
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "collections": [
      <a href="../document-entity-type#resource-representation">Document entity</a>
    ]
  }
}
</code></pre>

---

## documentURL

Get the document URL.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: documentURL
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "documentURL": string
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**documentURL**</td>
        <td>**string**</td>
        <td>The document URL.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## favorites

Add a Boolean flag indicating whether the document belongs to the user's Favorites.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: favorites
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "favorites": boolean
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**favorites**</td>
        <td>**boolean**</td>
        <td>Whether the document belongs to the user's Favorites.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## firstAccessibleAncestor

Get the closest accessible document's ancestor.

### Invokation


```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: firstAccessibleAncestor
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "firstAccessibleAncestor": <a href="../document-entity-type#resource-representation">Document entity</a>
  }
}
</code></pre>

---

## hasContent

Add a boolean flag indicating whether the document has children or members.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: hasContent
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "hasContent": boolean
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**hasContent**</td>
        <td>**boolean**</td>
        <td>Whether the document has children or members.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## hasFolderishChild

Add a boolean flag indicating whether the document has folderish children.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: hasFolderishChild
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "hasFolderishChild": boolean
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**favorites**</td>
        <td>**hasFolderishChild**</td>
        <td>Whether the document has folderish children.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## highlight

Get the [Elasticsearch highlights]({{page page='elasticsearch-highlights'}}) for a page provider.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/search/lang/pp/PAGE_PROVIDER_NAME
enrichers.document: highlight
```

### Resource Representation

```json
{
  "entity-type": "documents",
  "entries" : [
    {
      "entity-type": "document",
      "contextParameters": {
        "highlight": [
          {
            "field": string,
            "segments": [
              string
            ]
          }
        ]
      }
    }
  ],
  ...
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**field**</td>
        <td>**string**</td>
        <td>The highlight field.</td>
        <td></td>
      </tr>
      <tr>
        <td>**segments**</td>
        <td>**list**</td>
        <td>The list of segments with highlighted text for the given field.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## pendingTasks

Get the document pending tasks for the current user.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: pendingTasks
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "pendingTasks": [
      <a href="../task-entity-type#resource-representation">Task entity</a>
    ]
}
</code></pre>

---

## permissions

Get the permissions available for the current user.

###Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: permissions
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "permissions": [
      string
    ]
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**permissions**</td>
        <td>**list**</td>
        <td>The list of available permissions for the current user.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## preview

Get the preview URL.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: preview
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "preview": {
      "url": string
    }
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**url**</td>
        <td>**string**</td>
        <td>The document preview URL.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## publications

Get the document publications count.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: publications
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "publications": {
      "resultCount": long
    }
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**resultCount**</td>
        <td>**long**</td>
        <td>The document publications count.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## renditions

Get the document renditions.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: renditions
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "renditions": [
      {
        "name": string,
        "kind": string,
        "icon": string,
        "url": string
      }
    ]
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**name**</td>
        <td>**string**</td>
        <td>The rendition name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**kind**</td>
        <td>**string**</td>
        <td>The rendition kind.</td>
        <td></td>
      </tr>
      <tr>
        <td>**icon**</td>
        <td>**string**</td>
        <td>The rendition icon URL.</td>
        <td></td>
      </tr>
      <tr>
        <td>**url**</td>
        <td>**string**</td>
        <td>The rendition URL.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## runnableWorkflows

Get document runnable workflows for the current user.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: runnableWorkflows
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "runnableWorkflows": [
      <a href="../document-entity-type#resource-representation">Document entity</a>
    ]
}
</code></pre>

---

## runningWorkflows

Get document running workflows for the current user.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: runningWorkflows
```

### Resource Representation

<pre><code class="json hljs">{
  "entity-type": "document",
  ...
  "contextParameters": {
    "runningWorkflows": [
      <a href="../workflow-entity-type#resource-representation">Workflow entity</a>
    ]
}
</code></pre>

---

## subscribedNotifications

Get the current user subscribed notifications for the document.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: subscribedNotifications
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "subscribedNotifications": [
      string
    ]
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**subscribedNotifications**</td>
        <td>**list**</td>
        <td>The list of subscribed notifications.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## subtypes

Get the document allowed subtypes.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: subtypes
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "subtypes": [
      {
        "type": string,
        "facets": [
          string,
        ]
      }
    ]
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**type**</td>
        <td>**string**</td>
        <td>The subtype type.</td>
        <td></td>
      </tr>
      <tr>
        <td>**facets**</td>
        <td>**list**</td>
        <td>The subtype facets.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## tags

Get the document tags.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: tags
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "tags": [
      string
    ]
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**tags**</td>
        <td>**list**</td>
        <td>The list of tags.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## thumbnail

Get the document thumbnail URL.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: thumbnail
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "thumbnail": {
      "url": string
    }
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**url**</td>
        <td>**string**</td>
        <td>The thumbnail URL.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---

## userVisiblePermissions

Get the document user visible permissions.

### Invokation

```
GET https://NUXEO_SERVER/nuxeo/api/v1/id/DOC_ID
enrichers.document: userVisiblePermissions
```

### Resource Representation

```json
{
  "entity-type": "document",
  ...
  "contextParameters": {
    "userVisiblePermissions": [
      string
    ]
}
```

<div class="table-scroll">
  <table>
    <thead>
      <tr>
        <th>**Property Name**</th>
        <th>**Value**</th>
        <th>**Description**</th>
        <th>**Notes**</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>**userVisiblePermissions**</td>
        <td>**list**</td>
        <td>The document user visible permissions.</td>
        <td></td>
      </tr>
    </tbody>
  </table>
</div>

---
