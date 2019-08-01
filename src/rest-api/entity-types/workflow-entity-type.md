---
title: Workflow
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a [Workflow]({{page version='' space='nxdoc' page='workflow'}}).

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "workflow",
  "id": string,
  "name": string,
  "title": string,
  "state": string,
  "workflowModelName": string,
  "initiator": string | <a href="../user-entity-type#resource-representation">User entity</a>,
  "attachedDocumentIds": [
    { "id": string } | <a href="../document-entity-type#resource-representation">Document entity</a>
  ],
  "variables": object,
  "graphResource": string,
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
        <td>The entity type name. Value: the fixed string `"workflow"`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**id**</td>
        <td>**string**</td>
        <td>The workflow id.</td>
        <td></td>
      </tr>
      <tr>
        <td>**name**</td>
        <td>**string**</td>
        <td>The workflow name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**title**</td>
        <td>**string**</td>
        <td>The workflow title.</td>
        <td></td>
      </tr>
      <tr>
        <td>**state**</td>
        <td>**string**</td>
        <td>The workflow life cycle state.</td>
        <td></td>
      </tr>
      <tr>
        <td>**workflowModelName**</td>
        <td>**string**</td>
        <td>The workflow model name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**initiator**</td>
        <td>**string** <br /> or **object**</td>
        <td>
          The workflow initiator id.<br />
          Or the workflow initiator user entity, if the fetch property `initiator` is set.
        </td>
        <td></td>
      </tr>
      <tr>
        <td>**attachedDocumentIds**</td>
        <td>**list**</td>
        <td>
          The list of attached document ids.<br />
          Or the list of attached document entities, if the fetch property `attachedDocumentIds` is set.
        </td>
        <td></td>
      </tr>
      <tr>
        <td>**variables**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of workflow variables.</td>
        <td>Optional, present if the workflow is an instance.</td>
      </tr>
      <tr>
        <td>**graphResource**</td>
        <td>**string**</td>
        <td>The workflow graph resource URL.</td>
        <td>Optional, present if the workflow is an instance.</td>
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
