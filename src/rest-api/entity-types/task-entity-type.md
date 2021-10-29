---
title: Task
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a [Task]({{page version='' space='nxdoc' page='workflow'}}).

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "task",
  "id": string,
  "name": string,
  "workflowInstanceId": string,
  "workflowModelName": string,
  "workflowInitiator": string | <a href="../user-entity-type#resource-representation">User entity</a>,
  "workflowTitle": string,
  "workflowLifeCycleState": string,
  "graphResource": string,
  "state": string,
  "directive": string,
  "created": datetime,
  "dueDate": datetime,
  "nodeName": string,
  "targetDocumentIds": [
    string | <a href="../document-entity-type#resource-representation">Document entity</a>
  ],
  "actors": [
    { "id": string } | <a href="../user-entity-type#resource-representation">User entity</a>
  ],
  "delegatedActors": [
    { "id": string } | <a href="../user-entity-type#resource-representation">User entity</a>
  ],
  "comments": {
    "author": string,
    "text": string,
    "date": datetime
  },
  "variables": object,
  "taskInfo": {
    "allowTaskReassignment": boolean,
    "taskActions": [
      {
        "name": string,
        "url": string,
        "label": string,
        "validate": boolean
      }
    ]
  },
  "layoutResource": {
    "name": string,
    "url": string
  },
  "schemas": [
    {
      "name": string,
      "url": string
    }
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
      <td>The entity type name. Value: the fixed string `"task"`.</td>
      <td></td>
    </tr>
    <tr>
      <td>**id**</td>
      <td>**string**</td>
      <td>The task id.</td>
      <td></td>
    </tr>
    <tr>
      <td>**name**</td>
      <td>**string**</td>
      <td>The task name.</td>
      <td></td>
    </tr>
    <tr>
      <td>**workflowInstanceId**</td>
      <td>**string**</td>
      <td>The workflow instance id.</td>
      <td></td>
    </tr>
    <tr>
      <td>**workflowModelName**</td>
      <td>**string**</td>
      <td>The workflow model name.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**workflowInitiator**</td>
      <td>**string** <br /> or **object**</td>
      <td>
        The workflow initiator id.<br />
        Or the workflow initiator user entity, if the fetch property `workflowInitiator` is set.
      </td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**workflowTitle**</td>
      <td>**string**</td>
      <td>The workflow title.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**workflowLifeCycleState**</td>
      <td>**string**</td>
      <td>The workflow life cycle state.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**graphResource**</td>
      <td>**string**</td>
      <td>The workflow graph resource URL.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**state**</td>
      <td>**string**</td>
      <td>The task life cycle state.</td>
      <td></td>
    </tr>
    <tr>
      <td>**directive**</td>
      <td>**string**</td>
      <td>The task directive.</td>
      <td></td>
    </tr>
    <tr>
      <td>**created**</td>
      <td>**string**</td>
      <td>The time at which the task was created (W3C date-time).</td>
      <td></td>
    </tr>
    <tr>
      <td>**dueDate**</td>
      <td>**string**</td>
      <td>The time at which the task is due (W3C date-time).</td>
      <td></td>
    </tr>
    <tr>
      <td>**nodeName**</td>
      <td>**string**</td>
      <td>The task node name.</td>
      <td></td>
    </tr>
    <tr>
      <td>**targetDocumentIds[]**</td>
      <td>**list**</td>
      <td>
        The list of target document ids.<br />
        Or the list of target document entities, if the fetch property `targetDocumentIds` is set.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>**actors[]**</td>
      <td>**list**</td>
      <td>
        The list of actor ids.<br />
        Or the list of actor user entities, if the fetch property `actors` is set.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>**delegatedActors[]**</td>
      <td>**list**</td>
      <td>
        The list of delegated actor ids.<br />
        Or the list of delegated actor user entities, if the fetch property `actors` is set.
      </td>
      <td></td>
    </tr>
    <tr>
      <td>**comments[]**</td>
      <td>**list**</td>
      <td>The list of comments.</td>
      <td></td>
    </tr>
    <tr>
      <td>**comments[].author**</td>
      <td>**string**</td>
      <td>The comment author id.</td>
      <td></td>
    </tr>
    <tr>
      <td>**comments[].text**</td>
      <td>**string**</td>
      <td>The comment text.</td>
      <td></td>
    </tr>
    <tr>
      <td>**comments[].date**</td>
      <td>**datetime**</td>
      <td>The comment date (W3C date-time).</td>
      <td></td>
    </tr>
    <tr>
      <td>**variables**</td>
      <td>**object**</td>
      <td>A collection of key-value pairs of task variables.</td>
      <td></td>
    </tr>
    <tr>
      <td>**taskInfo**</td>
      <td>**object**</td>
      <td>The task information.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**taskInfo.allowTaskReassignment**</td>
      <td>**boolean**</td>
      <td>Whether the task can be reassigned.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**taskInfo.taskActions[]**</td>
      <td>**list**</td>
      <td>The list of task actions.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**taskInfo.taskActions[].name**</td>
      <td>**string**</td>
      <td>The action name.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**taskInfo.taskActions[].url**</td>
      <td>**string**</td>
      <td>The action URL.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**taskInfo.taskActions[].label**</td>
      <td>**string**</td>
      <td>The action label.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**taskInfo.taskActions[].validate**</td>
      <td>**boolean**</td>
      <td>Whether the action bypass validation.</td>
      <td>Optional</td>
    </tr>
    <tr>
      <td>**layoutResource**</td>
      <td>**object**</td>
      <td>The task layout resource.</td>
      <td></td>
    </tr>
    <tr>
      <td>**layoutResource.name**</td>
      <td>**string**</td>
      <td>The layout name.</td>
      <td></td>
    </tr>
    <tr>
      <td>**layoutResource.url**</td>
      <td>**string**</td>
      <td>The layout resource URL.</td>
      <td></td>
    </tr>
    <tr>
      <td>**schemas[]**</td>
      <td>**list**</td>
      <td>The list of task schemas.</td>
      <td></td>
    </tr>
    <tr>
      <td>**schemas[].name**</td>
      <td>**string**</td>
      <td>The schema name.</td>
      <td></td>
    </tr>
    <tr>
      <td>**schemas[].url**</td>
      <td>**string**</td>
      <td>The schema resource URL.</td>
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
