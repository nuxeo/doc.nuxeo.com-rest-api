---
title: Log Entry
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a Log Entry.

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "logEntry",
  "id": long,
  "category": string,
  "principalName": string,
  "comment": string,
  "docLifeCycle": string,
  "docPath": string,
  "docType": string,
  "docUUID": string,
  "eventId": string,
  "repositoryId": string,
  "eventDate": datetime,
  "logDate": datetime,
  "extended": object,
  "contextParameters": object
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
        <td>**entity-type**</td>
        <td>**string**</td>
        <td>The entity type name. Value: the fixed string `"logEntry"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**id**</td>
        <td>**long**</td>
        <td>The log entry id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**category**</td>
        <td>**string**</td>
        <td>The log entry category id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**principalName**</td>
        <td>**string**</td>
        <td>The log entry user.</td>
        <td></td>
      </tr>
      <tr>
        <td>**comment**</td>
        <td>**string**</td>
        <td>The log entry comment.</td>
        <td></td>
      </tr>
      <tr>
        <td>**docLifeCycle**</td>
        <td>**string**</td>
        <td>The log entry related document life cycle state.</td>
        <td></td>
      </tr>
      <tr>
        <td>**docPath**</td>
        <td>**string**</td>
        <td>The log entry related document path.</td>
        <td></td>
      </tr>
      <tr>
        <td>**docType**</td>
        <td>**string**</td>
        <td>The log entry related document type.</td>
        <td></td>
      </tr>
      <tr>
        <td>**docUUID**</td>
        <td>**string**</td>
        <td>The log entry relted document id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**eventId**</td>
        <td>**string**</td>
        <td>The log entry event id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**repositoryId**</td>
        <td>**string**</td>
        <td>The log entry repository name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**eventDate**</td>
        <td>**datetime**</td>
        <td>The log entry event date (ISO 8601 date-time).</td>
        <td></td>
      </tr>
      <tr>
        <td>**logDate**</td>
        <td>**datetime**</td>
        <td>The log entry insertion date (ISO 8601 date-time).</td>
        <td></td>
      </tr>
      <tr>
        <td>**extended**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of extended information.</td>
        <td></td>
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
