---
title: User
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a [User]({{page version='' space='userdoc' page='administration'}}#users-and-groups).

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "user",
  "id": string,
  "properties": object,
  "extendedGroups": [
    {
      "name": string,
      "label": string,
      "url": string
    }
  ],
  "isAdministrator": boolean,
  "isAnonymous": boolean,
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
        <td>The entity type name. Value: the fixed string `"user"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**id**</td>
        <td>**string**</td>
        <td>The user id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**properties**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of user properties.</td>
        <td></td>
      </tr>
      <tr>
        <td>**extendedGroups[]**</td>
        <td>**list**</td>
        <td>The list of user groups.</td>
        <td></td>
      </tr>
      <tr>
        <td>**extendedGroups[].name**</td>
        <td>**string**</td>
        <td>The group name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**extendedGroups[].label**</td>
        <td>**string**</td>
        <td>The group label.</td>
        <td></td>
      </tr>
      <tr>
        <td>**extendedGroups[].url**</td>
        <td>**string**</td>
        <td>The group resource URL.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isAdministrator**</td>
        <td>**boolean**</td>
        <td>Whether the user is an administrator.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isAnonymous**</td>
        <td>**boolean**</td>
        <td>Whether the user is anonymous.</td>
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
