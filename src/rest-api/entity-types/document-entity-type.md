---
title: Document
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
toc: false
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
  "properties": object,
  "facets": [
    string
  ],
  "contextParameters": object
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
        <td>**entity-type**</td>
        <td>**string**</td>
        <td>The entity type name. Value: the fixed string `"document"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**repository**</td>
        <td>**string**</td>
        <td>The document repository name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**uid**</td>
        <td>**string**</td>
        <td>The document id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**path**</td>
        <td>**string**</td>
        <td>The document path.</td>
        <td></td>
      </tr>
      <tr>
        <td>**type**</td>
        <td>**string**</td>
        <td>The document type.</td>
        <td></td>
      </tr>
      <tr>
        <td>**state**</td>
        <td>**string**</td>
        <td>The document life cyle state.</td>
        <td></td>
      </tr>
      <tr>
        <td>**parentRef**</td>
        <td>**string**</td>
        <td>The document parent id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isCheckedOut**</td>
        <td>**boolean**</td>
        <td>Whether the document is checked out.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isVersion**</td>
        <td>**boolean**</td>
        <td>Whether the document is a version.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isProxy**</td>
        <td>**boolean**</td>
        <td>Whether the document is a proxy.</td>
        <td></td>
      </tr>
      <tr>
        <td>**proxyTargetId**</td>
        <td>**string**</td>
        <td>The proxy source document id.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**versionableId**</td>
        <td>**string**</td>
        <td>The document version series id.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**changeToken**</td>
        <td>**string**</td>
        <td>The document current change token.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isTrashed**</td>
        <td>**boolean**</td>
        <td>Whether the document is trashed.</td>
        <td></td>
      </tr>
      <tr>
        <td>**title**</td>
        <td>**string**</td>
        <td>The document title.</td>
        <td></td>
      </tr>
      <tr>
        <td>**versionLabel**</td>
        <td>**string**</td>
        <td>The document version label.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**lockOwner**</td>
        <td>**string**</td>
        <td>The lock owner.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**lockCreated**</td>
        <td>**datetime**</td>
        <td>The lock creation date (ISO 8601 date-time).</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**lastModified**</td>
        <td>**datetime**</td>
        <td>The last time the document was modified (ISO 8601 date-time). Uses `dc:modified`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**properties**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of document properties.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**facets[]**</td>
        <td>**list**</td>
        <td>The document facets.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**contextParameters**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs filled by enabled enrichers.</td>
        <td>Optional</td>
      </tr>
    </tbody>
  </table>
</div>
