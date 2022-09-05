---
title: Stream Endpoint
review:
comment: ''
date: '2022-08-29'
status: ok
labels:
- http
- rest-api
  toc: true
  tree_item_index: 600
---

## Get List of Streams

```
GET /management/stream/streams
```

### Response

If successful, returns a JSON representation of all streams.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/stream/streams
```

```json
[
  {
    "name": "bulk/recomputeThumbnails",
    "partitions": 1,
    "codec": "avro"
  },
  {
    "name": "work/collections",
    "partitions": 12,
    "codec": "avro"
  },
  {
    "name": "bulk/zipBlob",
    "partitions": 2,
    "codec": "avro"
  },

    ...other streams...
]
```

## List Consumers of a Stream

```
GET /management/stream/consumers
```

### Query Parameters

| Parameter Name | Type       | Description      | Notes    |
|----------------| ---------- |------------------|----------|
| **stream**     | **string** | The stream name. | Required |


### Response

If successful, returns a JSON representation of the consumers for a given stream.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/stream/consumers?stream=bulk/command
```

```json
[
  {
    "stream": "bulk/command",
    "consumer": "bulk/scroller"
  }
]
```



## View Stream Content (Cat and Tail)

```
GET /management/stream/cat
```

### Query Parameters

| Parameter Name | Type        | Description                                                              | Notes    |
|----------------|-------------|--------------------------------------------------------------------------|----------|
| **stream**     | **string**  | The stream consumed by the consumer.                                     | Required |
| **limit**      | **integer** | The number of record to return.                                          | Optional |
| **fromGroup**  | **string**  | Use the position of the consumer as starting point.                      | Optional |
| **fromOffset** | **integer** | Use the offset as starting point, must be used with `partition` parameter | Optional |
| **partition**  | **integer** | View record for this partition.                                          | Optional |
| **rewind**     | **integer** | Go back a number of record from the request position.                    | Optional |
| **timeout**    | **string**  | Time to wait for new records, format is `10s` or `3min`.                    | Optional |


### Response

If successful, returns a Server-Sent Events (SSE) stream of JSON records. 

### Status Codes

- 200 _OK_ - Success.

### Sample

View 2 records from audit, the last processed and the next one:

```curl
curl -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/cat?stream=audit/audit&fromGroup=audit/writer&rewind=1&limit=2&timeout=1s"
```

```json
data: {"type":"lag","group":"audit/writer","stream":"audit/audit","partition":0,"lag":4,"pos":2668,"end":2672}

data: {"type":"seek","group":"admin/streamServlet","stream":"audit/audit","partition":0,"pos":2667,"end":2672}

data: {"type":"record","stream":"audit/audit","partition":0,"offset":2667,"watermark":"2022-09-05 13:06:01.159","key":"23","length":390,"message": {"entity-type":"logEntry","id":0,"category":"NuxeoAuthentication","principalName":"Administrator","comment":"Administrator successfully logged in using AUTOMATION_BASIC_AUTH authentication","docLifeCycle":null,"docPath":null,"docType":null,"docUUID":null,"eventId":"loginSuccess","repositoryId":null,"eventDate":"2022-09-05T13:06:01.159Z","logDate":"2022-09-05T13:06:01.159Z","extended":{}}}

data: {"type":"record","stream":"audit/audit","partition":0,"offset":2668,"watermark":"2022-09-05 13:06:29.707","key":"24","length":390,"message": {"entity-type":"logEntry","id":0,"category":"NuxeoAuthentication","principalName":"Administrator","comment":"Administrator successfully logged in using AUTOMATION_BASIC_AUTH authentication","docLifeCycle":null,"docPath":null,"docType":null,"docUUID":null,"eventId":"loginSuccess","repositoryId":null,"eventDate":"2022-09-05T13:06:29.707Z","logDate":"2022-09-05T13:06:29.707Z","extended":{}}}

data: {"type":"disconnect","message":"Limit reached, bye."}
```

Tail on the bulk command stream:
```curl
curl -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/cat?stream=bulk/command&fromGroup=bulk/scroller&rewind=1&timeout=60s"
```

```json
data: {"type":"lag","group":"bulk/scroller","stream":"bulk/command","partition":0,"lag":0,"pos":2,"end":2}

data: {"type":"lag","group":"bulk/scroller","stream":"bulk/command","partition":1,"lag":0,"pos":2,"end":2}

data: {"type":"seek","group":"admin/streamServlet","stream":"bulk/command","partition":0,"pos":1,"end":2}

data: {"type":"seek","group":"admin/streamServlet","stream":"bulk/command","partition":1,"pos":1,"end":2}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"record","stream":"bulk/command","partition":0,"offset":2,"watermark":"2022-09-05 13:16:02.214","key":"4eec2cb5-7470-48ec-8b63-bb2a43c1e847","length":137,"message": {"avroSchema":"BulkCommand","id": "4eec2cb5-7470-48ec-8b63-bb2a43c1e847", "action": "index", "query": "SELECT ecm:uuid FROM Document", "queryLimit": null, "username": "Administrator", "repository": "default", "bucketSize": 1000, "batchSize": 25, "batchTransactionTimeout": 0, "scroller": null, "genericScroller": false, "externalScroller": false, "params": "{\"updateAlias\":true}"}}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"record","stream":"bulk/command","partition":1,"offset":2,"watermark":"2022-09-05 13:16:29.896","key":"ada44abc-3bf2-4130-8ddb-7bed2aeaf2a2","length":437,"message": {"avroSchema":"BulkCommand","id": "ada44abc-3bf2-4130-8ddb-7bed2aeaf2a2", "action": "csvExport", "query": "SELECT * FROM Document WHERE ecm:primaryType NOT IN ('Domain', 'SectionRoot', 'TemplateRoot', 'WorkspaceRoot', 'Favorites') AND ecm:mixinType != 'HiddenInNavigation' AND NOT (ecm:mixinType = 'Collection' AND ecm:name = 'Locally Edited') AND ecm:isVersion = 0 AND ecm:isTrashed = 0 AND ecm:parentId IS NOT NULL AND ecm:uuid IS NOT NULL", "queryLimit": 100000, "username": "Administrator", "repository": "default", "bucketSize": 100, "batchSize": 50, "batchTransactionTimeout": 0, "scroller": "elastic", "genericScroller": false, "externalScroller": false, "params": null}}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}

data: {"type":"connect","message":"keepalive"}
  
data: {"type":"disconnect","message":"Read timeout, bye."}
```

Note that there is a JSP page that gives a demonstration of this `cat` endpoint, it requires `Administrator` privilege:

[http://localhost:8080/nuxeo/stream.jsp](http://localhost:8080/nuxeo/stream.jsp)


## Get Detailed Nuxeo Stream and Processor Information
```
GET /management/stream
```


### Query Parameters

| Parameter Name | Type       | Description                                | Notes    |
|----------------| ---------- |--------------------------------------------|----------|
| **format**     | **string** | The output format, only puml is supported. | Optional |

Default format is JSON representation, a Plant UML output can be requested.

### Response

Returns a JSON representation of all available Nuxeo Stream information:
- a list of streams
- the list of deployed Stream processors and topologies
- all related metrics

The format parameter enables to ask for a graphical Plant UML representation instead of JSON.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/stream/
```

```json
{
  "streams": [
    {
      "name": "bulk/recomputeThumbnails",
      "partitions": 1,
      "codec": "avro"
    },
      ... list of streams ...
    ],
  "processors": [
    {
      "metadata": {
        "hostname": "nuxeo",
        "cpuCores": "16",
        "ip": "172.26.0.10",
        "processorName": "auditWriter",
        "jvmHeapSize": "2147483648"
      },
      "computations": [
        {
          "name": "audit/writer",
          "threads": 1,
          "continueOnFailure": false,
          "batchCapacity": 25,
          "batchThresholdMs": 500,
          "maxRetries": 20,
          "retryDelayMs": 1000
        }
      ],
      "topology": [
        [
          "stream:audit/audit",
          "computation:audit/writer"
        ]
      ]
    },
      ... list of all processors ...
    ],
  "metrics": [
    {
      "timestamp": 1662371154,
      "hostname": "nuxeo",
      "ip": "192.168.176.10",
      "nodeId": null,
      "metrics": [
        {
          "k": "nuxeo.streams.global.stream.group.end",
          "group": "audit-writer",
          "stream": "audit-audit",
          "v": 2645
        }, ... 
        {
          "k": "nuxeo.streams.computation.processRecord",
          "computation": "work-common",
          "count": 18,
          "rate1m": 0.0152098206590408,
          "rate5m": 0.009001128456818261,
          "sum": 19194601,
          "max": 0.001976188,
          "mean": 5.094094203003321E-4,
          "min": 4.70333E-4,
          "stddev": 1.5061167728046484E-5,
          "p50": 5.09072E-4,
          "p95": 5.09072E-4,
          "p99": 5.89058E-4

        },
        ... list of all metrics for all nodes ...
        ]
      }
    ]
}
```

Generate a graphical representation of the Stream processing: 

```curl
# Get Plant UML JAR (it requires Graphviz see https://plantuml.com/faq-install for more info)
curl https://netcologne.dl.sourceforge.net/project/plantuml/plantuml.jar -o /tmp/plantuml.jar 

# Get the Plant UML representation of the Nuxeo Streams
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/stream/?format=puml -o /tmp/streams.puml

# Generate a SVG
java  -DPLANTUML_LIMIT_SIZE=16384  -jar /tmp/plantuml.jar /tmp/streams.puml -tsvg

# view it
x-www-browser /tmp/streams.svg
```


## Get Consumer Positions

```
GET /management/stream/consumer/position
```


### Query Parameters

| Parameter Name | Type       | Description                                             | Notes    |
|----------------| ---------- |---------------------------------------------------------|----------|
| **stream**     | **string** | The stream consumed by the consumer.                    | Required |
| **consumer**   | **string** | The consumer name. | Required |

### Response

Returns a JSON representation of the current consumer position.

### Status Codes
- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/position?stream=audit/audit&consumer=audit/writer"
```

```json
{
  "stream": "audit/audit",
  "consumer": "audit/writer",
  "lag": 1,
  "lags": [
    {
      "partition": 0,
      "pos": 2648,
      "end": 2649,
      "lag": 1
    }
  ]
}
```

```curl
curl -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/position?stream=work/common&consumer=work/common"
```

```json
{
  "stream": "work/common",
  "consumer": "work/common",
  "lag": 0,
  "lags": [
    {
      "partition": 0,
      "pos": 1107,
      "end": 1107,
      "lag": 0
    },
    {
      "partition": 1,
      "pos": 1162,
      "end": 1162,
      "lag": 0
    },
    {
      "partition": 2,
      "pos": 1195,
      "end": 1195,
      "lag": 0
    },
    {
      "partition": 3,
      "pos": 1182,
      "end": 1182,
      "lag": 0
    },
    {
      "partition": 4,
      "pos": 1100,
      "end": 1100,
      "lag": 0
    },
    {
      "partition": 5,
      "pos": 1162,
      "end": 1162,
      "lag": 0
    }
  ]
}
```



## Stop a Consumer Thread Pool on All Nuxeo Nodes

```
PUT /management/stream/consumer/stop
```

### Query Parameters

| Parameter Name | Type       | Description                                             | Notes    |
|----------------| ---------- |---------------------------------------------------------|----------|
| **consumer**   | **string** | The consumer name. | Required |

### Response

Always 204, this stops all consumer threads on all Nuxeo nodes of the clusters, the effective stop of the threads
can take few seconds after returning.

### Status Codes

- 204 _NO_CONTENT_ 

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/stop?consumer=audit/writer"
```
 
This operation is traced at WARN level on all Nuxeo nodes running a consumer thread pool:
```log
WARN  [LogStreamProcessor] Stopping computation thread pool: Name{id='audit-writer', urn='audit/writer'}
```

## Start Consumer Thread Pool on All Nuxeo Nodes

```
PUT /management/stream/consumer/start
```

### Query Parameters

| Parameter Name | Type       | Description                                             | Notes    |
|----------------| ---------- |---------------------------------------------------------|----------|
| **consumer**   | **string** | The consumer name. | Required |

### Response

Always 204, this start a consumer threads pools (previously stopped) on all Nuxeo nodes of the clusters.

### Status Codes

- 204 _NO_CONTENT_

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/start?consumer=audit/writer"
```

This is traced at WARN level on all Nuxeo logs:
```log
WARN  [LogStreamProcessor] Starting computation thread pool: Name{id='audit-writer', urn='audit/writer'}
```


## Change Consumer Position to End of the Stream

```
PUT /management/stream/consumer/position/end
```

### Query Parameters

| Parameter Name | Type       | Description        | Notes    |
|----------------| ---------- |--------------------|----------|
| **consumer**   | **string** | The consumer name. | Required |
| **stream**     | **string** | The stream name.   | Required |

### Response

The consumer thread pool must be first stopped with the `/management/stream/consumer/stop` endpoint.
Move the position to the end of the stream and returns a JSON representation of the consumer position before
and after the move.

### Status Codes

- 409 _CONFLICT_ - When consumers are not stopped 
- 200 _OK_ - Success.

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/position/end?consumer=audit/writer&stream=audit/audit"
```

```json
{
  "before": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 2,
    "lags": [
      {
        "partition": 0,
        "pos": 2658,
        "end": 2660,
        "lag": 2
      }
    ]
  },
  "after": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 0,
    "lags": [
      {
        "partition": 0,
        "pos": 2660,
        "end": 2660,
        "lag": 0
      }
    ]
  }
}
```


## Change Consumer Position to the Beginning of the Stream

```
PUT /management/stream/consumer/position/beginning
```

### Query Parameters

| Parameter Name | Type       | Description        | Notes    |
|----------------| ---------- |--------------------|----------|
| **consumer**   | **string** | The consumer name. | Required |
| **stream**     | **string** | The stream name.   | Required |

### Response

The consumer thread pool must be first stopped with the `/management/stream/consumer/stop` endpoint.
Move the position to the beginning of the stream and returns a JSON representation of the consumer position before
and after the move.

### Status Codes

- 409 _CONFLICT_ - When consumers are not stopped
- 200 _OK_ - Success.

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/position/beginning?consumer=audit/writer&stream=audit/audit"
```

```json
{
  "before": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 1,
    "lags": [
      {
        "partition": 0,
        "pos": 2661,
        "end": 2662,
        "lag": 1
      }
    ]
  },
  "after": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 20,
    "lags": [
      {
        "partition": 0,
        "pos": 2642,
        "end": 2662,
        "lag": 20
      }
    ]
  }
}
```


## Change Consumer Position to a Specific Offset 

```
PUT /management/stream/consumer/position/offset
```

### Query Parameters

| Parameter Name | Type        | Description           | Notes    |
|----------------|-------------|-----------------------|----------|
| **consumer**   | **string**  | The consumer name.    | Required |
| **stream**     | **string**  | The stream name.      | Required |
| **partition**  | **integer** | The partition number. | Required |
| **offset**     | **long**    | The offset value.     | Required |

### Response

The consumer thread pool must be first stopped with the `/management/stream/consumer/stop` endpoint.
Move the position for a specific partition to the exact offset and returns a JSON representation of the consumer position before
and after the move.

### Status Codes

- 409 _CONFLICT_ - When consumers are not stopped
- 200 _OK_ - Success.

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/position/offset?consumer=audit/writer&stream=audit/audit&partition=0&offset=2652"
```

```json
{
  "before": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 21,
    "lags": [
      {
        "partition": 0,
        "pos": 2642,
        "end": 2663,
        "lag": 21
      }
    ]
  },
  "after": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 11,
    "lags": [
      {
        "partition": 0,
        "pos": 2652,
        "end": 2663,
        "lag": 11
      }
    ]
  }
}
```


## Change Consumer Position After a Given Date

```
PUT /management/stream/consumer/position/after
```

### Query Parameters

| Parameter Name | Type       | Description                                                               | Notes    |
|----------------|------------|---------------------------------------------------------------------------|----------|
| **consumer**   | **string** | The consumer name.                                                        | Required |
| **stream**     | **string** | The stream name.                                                          | Required |
| **date**       | **string** | The date in ISO-8601 format, for instance `2022-09-05T12:49:34.308625Z`. | Required |

### Response

The consumer thread pool must be first stopped with the `/management/stream/consumer/stop` endpoint.
Move the position to record that were appended to the stream just after the given date and returns a JSON representation of the consumer position before
and after the move.

### Status Codes
- 
- 409 _CONFLICT_ - When consumers are not stopped
- 200 _OK_ - Success.

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
"http://localhost:8080/nuxeo/api/v1/management/stream/consumer/position/after?consumer=audit/writer&stream=audit/audit&date=2022-09-05T10:00:00Z"
```

```json
{
  "before": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 15,
    "lags": [
      {
        "partition": 0,
        "pos": 2652,
        "end": 2667,
        "lag": 15
      }
    ]
  },
  "after": {
    "stream": "audit/audit",
    "consumer": "audit/writer",
    "lag": 19,
    "lags": [
      {
        "partition": 0,
        "pos": 2648,
        "end": 2667,
        "lag": 19
      }
    ]
  }
}
```
