---
title: Bulk Status Entity Type
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

Representation of a Bulk Status.

## Resource Representation

<pre><code class="json hljs">{
  "entity-type": "bulkStatus",
  "commandId": string,
  "state": string,
  "processed": long,
  "error": boolean,
  "errorCount": long,
  "total": long,
  "action": string,
  "username": string,
  "submitted": datetime,
  "scrollStart": long,
  "scrollEnd": long,
  "processingStart": long,
  "processingEnd": long,
  "completed": long,
  "processingMillis": long
}
</code></pre>
