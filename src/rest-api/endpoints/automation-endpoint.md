---
title: Automation
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
    - todo
    - automation
    - endpoint
    - excerpt
toc: true
tree_item_index: 100
---
<!--
// TODO
-->
## The Automation HTTP / REST Service

{{! excerpt}}
The Nuxeo Automation Server module provides a REST API to execute operations on a Nuxeo server.
{{! /excerpt}}

{{#> callout type='info' heading='About Automation'}}
To learn more about Content Automation, see the [Automation documentation]({{page page='automation'}}). This section only deals with REST exposition of operations and automation chains.
{{/callout}}

To use the Automation REST service, you need the URL where the service is exposed, and the different formats used by the service to exchange information. All other URLs that appear in content exchanged between the client and server are relative paths to the Automation service URL.

Operations context and parameters, as well as response objects (documents), are formatted as JSON objects. To transport blobs, HTTP multipart requests should be used to attach blob binary data along with the JSON objects describing the operation request.

The REST service is bound to the `http://NUXEO_SERVER/nuxeo/site/automation` path. To get the service description, you should do a GET on the service URL using an Accept type of `application/json+nxautomation`. You will get the service description as a response in the form of a JSON document. This document will contain the list of available operations and automation chains, as well as the URLs for other optional services provided (like login or document type service).

By default, all the chains and operations that are not UI related are accessible through REST. You can filter the set of exposed operations and chains or protect them using security rules. For more details on this see [Filtering Exposed Operations]({{page page='filtering-exposed-operations'}}).

{{#> callout type='info' }}
You do not need to be logged in to be able to get the Automation service description.
{{/callout}}

## Executing Operations

The operations registry (loaded by performing a GET on the Automation service URL) contains all the information you need to execute operations.

To execute an operation, build an operation request descriptor and POST it on the operation URL. When sending an operation request, you must use the `application/json+nxrequest` content type (`application/json` from 5.9.5 is allowed as well). You need to authenticate your request using basic authentication since most of the operations are accessing the Nuxeo repository.

An operation request is a JSON document with the following format:

```
  input: "the_operation_input_object_reference",
  params: {key1: "value1", key: "value2", ...},
  context: {key1: "val1", ... }

```

These three request parameters are optional and depend on the executed operation.

- If the operation has no input (a void operation), the `input` parameter can be omitted.
- If the operation has no parameters, `params` can be omitted.
- If the operation does not push specific properties to the operation execution context, then context can be omitted.

The `input` parameter is a string that acts as a reference to the real object to be used as the input. There are four types of supported inputs: void, document, document list, blob, blob list.

### Request Input

- To reference a **document**, use the document absolute path or document UID preceded by the string `doc:`.</br>
  For example:
  `doc:/default-domain/workspaces/myworkspace` or `doc:96bfb9cb-a13d-48a2-9bbd-9341fcf24801`


- To reference a **document list** use a comma-separated list of absolute document paths or UIDs preceded by the string `docs:`. </br>
  For example:
  `docs:/default-domain/workspaces/myworkspace, 96bfb9cb-a13d-48a2-9bbd-9341fcf24801`


- A **blob** cannot be referenced by a string locator as it is usually on the client file system or as raw binary data. You must therefore use a `multipart/related` request that encapsulates your JSON request as the root part as `application/json+nxrequest` content and the blob binary content in a related part.


- For a **blob list**, simply add one additional content part for each blob in the list.


  The only limitation for both blobs and blob lists, is that the request content part should be the first part in the multipart document. The order of the blob parts will be preserved and blobs will be processed in the same order. The server assumes the request part to be the first part of the multipart document (Content-Ids are not used by the server to identify the request part).

### Request Parameter Types

The operation parameters in the `params` property of the request are **strings**. Operation parameters are typed, so on the server-side the operation will know how to decode parameters in real Java classes. The supported parameter types are: **string**, **long** (integer number), **double** (floating point number), **date**, **properties**, **document**, **documents**, **EL expression**, **EL template**.

Here are some rules on how to encode operation parameters:

- `string`: Let it as is.
- `long`: Just use a string representation of the number (in Java `Long.toString()`).
- `double`: Just use a string representation of the number (in Java `Double.toString()`).
- `date`: Use the W3C format (UTC timezone preferred).
- `boolean`: "true" or "false".
- `document`: Use the document UID or the absolute document path.
- `documents`: Use a comma-separated list of document references.
- **EL expression**: Put the `expr:` string before your EL expression. (`expr: Document.path`).
- **EL template**: Put the `expr:` string before your template. (`expr: SELECT * FROM Document WHERE dc:title=@{my_var}`)

    Note that in EL expressions you must also specify relative paths (relative to the context document) using `expr: ./my/doc`.

All these encoding rules are the same as those used when defining operation chains in Nuxeo XML extensions.

## Operation Execution Response

An operation can have one of the following outputs:

<div class="table-scroll">
  <table class="hover">
    <tbody>
      <tr>
        <th colspan="1">Output</th>
        <th class="small-2">Type</th>
        <th colspan="1">HTTP Response</th>
      </tr>
      <tr>
        <td colspan="1">**void**</td>
        <td class="small-2">The operation has no output</td>
        <td colspan="1">Returns HTTP 204. No content and no Content-Type is returned.</td>
      </tr>
      <tr>
        <td colspan="1">**document**</td>
        <td class="small-2">A repository document</td>
        <td colspan="1">Returns a JSON object describing the document. Content-Type is `application/json`</td>
      </tr>
      <tr>
        <td colspan="1">**document list**</td>
        <td class="small-2">A list of documents</td>
        <td colspan="1">Returns a JSON object describing the list of documents. Content-Type is `application/json`</td>
      </tr>
      <tr>
        <td colspan="1">**blob**</td>
        <td class="small-2">Binary content usually attached to a document</td>
        <td colspan="1">Returns the blob raw content. Content-Type is the same as the blob mime-type.</td>
      </tr>
      <tr>
        <td colspan="1">**blob list**</td>
        <td class="small-2">A list of blobs</td>
        <td colspan="1">Returns a Multipart/Mixed content. Each part is a blob from the list (order is preserved) and uses the same Content-Type as the blob mime-type.</td>
      </tr>
      <tr>
        <td colspan="1">**exception**</td>
        <td class="small-2"></td>
        <td colspan="1">Returns HTTP 400. The content is the server exception encoded as a JSON object. The used Content-Type is `application/json`. When an exception occurs, the server tries to return a meaningful status code. If no suitable status code is found, a generic 500 code (server error) is used.</td>
      </tr>
    </tbody>
  </table>
</div>

### Document

Each time returned objects are encoded as JSON objects, the `application/json` Content-Type is used. Only **document**, **documents** and **exception** objects are encoded as JSON.

A JSON **document** entity contains the minimum required information about the document as top-level entries.

These entries are always set on any document and use the following keys:

<div class="table-scroll">
  <table class="hover">
    <tbody>
      <tr>
        <td>`uid`</td>
        <td>Document UID</td>
      </tr>
      <tr>
        <td>`path`</td>
        <td>Document path in the repository</td>
      </tr>
      <tr>
        <td>`type`</td>
        <td>Document type</td>
      </tr>
      <tr>
        <td>`state`</td>
        <td>Current lifecycle state</td>
      </tr>
      <tr>
        <td>`title`</td>
        <td>Document title</td>
      </tr>
      <tr>
        <td>`lastModified`</td>
        <td>Last modified timestamp</td>
      </tr>
    </tbody>
  </table>
</div>

All the other document properties are contained within a "properties" map using the property XPath as the key for the top-level entries.

Complex properties are represented as embedded JSON objects and list properties as embedded JSON arrays.

{{#> callout type='info' }}
All `application/json` JSON entities always contains a required top-level property: `entity-type`.
This property is used to identify which type of object is described:
- `document`
- `documents`
- `exception`
{{/callout}}

Example of a JSON **document** entry:

```
{
  "entity-type": "document",
  "uid": "96bfb9cb-a13d-48a2-9bbd-9341fcf24801",
  "path": "/default-domain/workspaces/myws/file",
  "type": "File",
  "state": "project",
  "title": "file",
  "lastModified": "2010-05-24T15:07:08Z",
  "properties":   {
    "uid:uid": null,
    "uid:minor_version": "0",
    "uid:major_version": "1",
    "dc:creator": "Administrator",
    "dc:contributors": ["Administrator"],
    "dc:source": null,
    "dc:created": "2010-05-22T08:42:56Z",
    "dc:description": "",
    "dc:rights": null,
    "dc:subjects": [],
    "dc:valid": null,
    "dc:format": null,
    "dc:issued": null,
    "dc:modified": "2010-05-24T15:07:08Z",
    "dc:coverage": null,
    "dc:language": null,
    "dc:expired": null,
    "dc:title": "file",
    "files:files": [],
    "common:icon": null,
    "common:icon-expanded": null,
    "common:size": null,
    "file:content":     {
      "name": "test.jpg",
      "mime-type": "image/jpeg",
      "encoding": null,
      "digest": null,
      "length": "290096",
      "data": "files/96bfb9cb-a13d-48a2-9bbd-9341fcf24801?path=%2Fcontent"
    },
    "file:filename": null
  }

```

The top-level properties `title` and `lastModified` have the same value as the corresponding embedded properties `dc:title` and `dc:modified`.

{{#> callout type='info' }}
Blob data, instead of containing raw data, contain a relative URL that can be used to retrieve the real data of the blob (using a GET request on that URL).
{{/callout}}

### Documents

The **documents** JSON entity is a list of JSON document entities and has the entity type `documents`. The documents in the list contain only the required top-level properties.

Example:

```
{
  entity-type: "documents"
  entries: [
   {
     "entity-type": "document",
     "uid": "96bfb9cb-a13d-48a2-9bbd-9341fcf24801",
     "path": "/default-domain/workspaces/myws/file",
     "type": "File",
     "state": "project",
     "title": "file",
     "lastModified": "2010-05-24T15:07:08Z",
   },
   ...
   ]
 }

```

### Exception

The **exception** JSON entities have an `exception` entity type and contain information about the exception including the server stack trace if the extended mode is activated, see [Error Handling]({{page page='error-handling'}})

Example:

```
{
  "entity-type": "exception",
  "status": 500,
  "message": "Failed to execute operation: Blob.Attach",
  "stack": "org.nuxeo.ecm.automation.OperationException: Failed to invoke operation Blob.Attach\n\tat org.nuxeo.ecm.automation.core.impl.InvokableMethod.invoke(InvokableMethod.java:143)\n\t ..."
}

```

## Document Property Types

Property values can be of one of these types:

- `string`
- `long`: Encoded as a string representation of the number (in Java: `Long.toString()`)
- `double`: Encoded as a string representation of the number (in Java: `Double.toString()`)
- `date`: Encoded as a W3C format (UTC timezone preferred)
- `boolean`: "true" or "false"

    For **null** values the JSON `null` keyword is used.

Of further note on the JSON document entity format:

- A document entity uses **string** values for any scalar property value.
- Dates are encoded as **W3C dates** (in UTC timezone).
- Apart from strings, you may have **null** values for properties that are not set (but are defined by the schema), **JSON objects** (maps) for complex properties, and **JSON arrays** for array or list properties.
- Blob data is encoded as a relative URL (relative to Automation service URL) from where you can download the raw data of the blob (using a GET request on that URL).

## Operation vs. Transactions

The server runs an operation or operation chain in a single transaction. A rollback is done if the operation execution results in an exception.

The transaction is committed when the operation (or operation chain) has successfully terminated.

Operations can be executed in two different contexts: either in the context of a stateful repository session or one session per operation.

By default, operations reuse the same session if your client supports cookies (even in basic authentication).

To enable stateless sessions, you need to modify some Nuxeo configuration. In stateless mode, the session is closed at the end of the request.

Note that Automation service uses Nuxeo WebEngine for HTTP request management.

## Operation Security

Some operations can only be executed by some users or groups. This is defined on the server side through Nuxeo XML extensions.

See [Filtering Exposed Operations]({{page page='filtering-exposed-operations'}}) for more details.

## Examples

### Getting the Automation Service

Request for service description:

```
GET http://NUXEO_SERVER/nuxeo/site/automation
Accept: application/json+nxautomation
```

Response:

```
HTTP/1.1 200 OK
Content-Type: application/json+nxautomation

```

```
{
  "paths": {"login" : "login"},
  "operations": [
      "id" : "Blob.Attach",
      "label": "Attach File",
      "category": "Files",
      "description": "Attach the input file to the document given as a parameter. If the xpath points to a blob list then the blob is appended to the list, otherwise the xpath should point to a blob property. If the save parameter is set the document modification will be automatically saved. Return the blob.",
      "url": "Blob.Attach",
      "signature": [ "blob", "blob" ],
      "params": [
         {
           "name": "document",
            "type": "document",
            "required": true,
            "values": []
         },
         {
           "name": "save",
           "type": "boolean",
           "required": false,
           "values": ["true"]
         },
         {
           "name": "xpath",
           "type": "string",
           "required": false,
           "values": ["file:content"]
         }
      ]
  // ... other operations follow here
  ],
  "chains" : [
    // a list of operation chains (definition is identical to regular operations)
  ]
}

```

You can see the automation service is returning the registry of operations and chains available on the server.

Each operation and chain signature is fully described in order to permit operation validation client-side. Additional information is provided which can be used in a UI (operation label, full description, operation category, etc.).

The `url` property of an operation or automation chain is the relative path to use to execute the operation. For the service URL `http://NUXEO_SERVER/nuxeo/site/automation` and the `Blob.Attach` operation with the `url` `Blob.Attach`, the complete URL for the operation would be: `http://NUXEO_SERVER/nuxeo/site/automation/Blob.Attach`.

The `paths` property is used to specify various relative paths (relative to the automation service) of services exposed by the automation server. In the above example you can see that the `login` service is using the relative path `login`.

This service can be used to sign in and check if the username/password is valid. To use this service you should do a POST to the login URL (`http://NUXEO_SERVER/nuxeo/site/automation/login`) using basic authentication. If authentication fails you will receive a 401 HTTP response. Otherwise the 200 code is returned.

The login service can be used to log in and validate a user login.

Note that `WWW-Authenticate` server response is not yet implemented so you need to send the basic authentication header in each call if you are not using cookies. You only need to authenticate once if you're using cookies - for example using the login service.

### Invoking A Simple Operation

```
POST http://NUXEO_SERVER/nuxeo/site/automation/Document.Fetch HTTP/1.1
Accept: application/json, */*
Content-Type: application/json+nxrequest; charset=UTF-8
Authorization: Basic QWRtaW5pc3RyYXRvcjpBZG1pbmlzdHJhdG9y
Host: localhost:8080

```

### Taking a Blob as Input

Here is an example invoking the `Blob.Attach` operation on a document given by its path (`/default-domain/workspaces/myws/file` in our example).

```
POST http://NUXEO_SERVER/nuxeo/site/automation/Blob.Attach HTTP/1.1
Accept: application/json, */*
Content-Type: multipart/related;
    boundary="----=_Part_0_130438955.1274713628403"; type="application/json+nxrequest"; start="request"
Authorization: Basic QWRtaW5pc3RyYXRvcjpBZG1pbmlzdHJhdG9y
Host: localhost:8080

```

```
------=_Part_0_130438955.1274713628403
Content-Type: application/json+nxrequest; charset=UTF-8
Content-Transfer-Encoding: 8bit
Content-ID: request
Content-Length: 75

{"params":{"document":"/default-domain/workspaces/myws/file"},"context":{}}

------=_Part_0_130438955.1274713628403
Content-Type: image/jpeg
Content-Transfer-Encoding: binary
Content-Disposition: attachment; filename=test.jpg
Content-ID: input

[binary data comes here]

------=_Part_0_130438955.1274713628403--

```

In both examples you can see that the following `Accept` header is used:
`Accept: application/json, **/**`.

This header is necessary because it specifies that the client accept as a response either a JSON encoded entity or a blob that may have any type. The `application/json` is the first content type to help the server choose the format of the response when returning an encoded object.


```
{"params":{"value":"/default-domain/workspaces/myws/file"},"context":{}}

```

This operation will return the document content specified by the `value` parameter.

## Learn More

- Learn about the [Content Automation Concepts]({{page page='content-automation-concepts'}}).
- Test the `/automation` endpoint on your local instance with the [Nuxeo API Playground](http://nuxeo.github.io/api-playground/), see [documentation]({{page page='nuxeo-api-playground'}}).
