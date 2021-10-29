---
title: Directory
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a [Directory]({{page version='' space='nxdoc' page='data-lists-and-directories'}}).

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "directory",
  "name": string,
  "schema": string,
  "idField": string,
  "parent": string,
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
        <td>The entity type name. Value: the fixed string `"directory"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**name**</td>
        <td>**string**</td>
        <td>The directory name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**schema**</td>
        <td>**string**</td>
        <td>The directory schema name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**idField**</td>
        <td>**string**</td>
        <td>The directory id field name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**parent**</td>
        <td>**string**</td>
        <td>The parent directory name.</td>
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
