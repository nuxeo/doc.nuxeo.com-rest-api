---
title: Directory Entry Entity Type
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a Directory Entry.

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "directoryEntry",
  "directoryName": string,
  "id": string,
  "properties": object,
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
        <td>The entity type name. Value: the fixed string `"directoryEntry"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**directoryName**</td>
        <td>**string**</td>
        <td>The directory name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**id**</td>
        <td>**string**</td>
        <td>The directory entry id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**properties**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of directory entry properties.</td>
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
