---
title: Group Entity Type
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a Group.

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "group",
  "id": string,
  "properties": object,
  "memberUsers": [
    string
  ],
  "memberGroups": [
    string
  ],
  "parentGroups": [
    string
  ],
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
        <td>The entity type name. Value: the fixed string `"group"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**id**</td>
        <td>**string**</td>
        <td>The group id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**properties**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of group properties.</td>
        <td></td>
      </tr>
      <tr>
        <td>**memberUsers[]**</td>
        <td>**list**</td>
        <td>The list of group member user ids, if the fetch property `memberUsers` is set.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**memberGroups[]**</td>
        <td>**list**</td>
        <td>The list of group member group ids, if the fetch property `memberGroups` is set.</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**parentGroups[]**</td>
        <td>**list**</td>
        <td>The list of group parent group ids, if the fetch property `parentGroups` is set.</td>
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
