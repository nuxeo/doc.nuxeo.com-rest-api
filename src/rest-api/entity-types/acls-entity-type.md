---
title: ACLs
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a list of [ACLs]({{page version='' space='nxdoc' page='acls'}}) (Access Control List).

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "acls",
  "acls": [
    {
      "name": string,
      "ace": [
        {
          "id": string,
          "username": string,
          "permission": string,
          "granted": boolean,
          "creator": string,
          "begin": datetime,
          "end": datetime,
          "status":string
        }
      ]
    }
  ]
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
        <td>The entity type name. Value: the fixed string `"acls"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[]**</td>
        <td>**list**</td>
        <td>The list of ACLs (Access Control List).</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].name**</td>
        <td>**string**</td>
        <td>The ACL name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[]**</td>
        <td>**list**</td>
        <td>The list of the ACL ACEs (Access Control Entry).</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].id**</td>
        <td>**string**</td>
        <td>The ACE id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].username**</td>
        <td>**string**</td>
        <td>The ACE username.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].permission**</td>
        <td>**string**</td>
        <td>The ACE permission.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].granted**</td>
        <td>**boolean**</td>
        <td>Whether the ACE is granted.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].creator**</td>
        <td>**string**</td>
        <td>The ACE creator.</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].begin**</td>
        <td>**datetime**</td>
        <td>The ACE begin date (W3C date-time).</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].end**</td>
        <td>**datetime**</td>
        <td>The ACE end date (W3C date-time).</td>
        <td></td>
      </tr>
      <tr>
        <td>**acls[].ace[].status**</td>
        <td>**string**</td>
        <td>The ACE status. Value: `pending`, `effective` or `archived`.</td>
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
