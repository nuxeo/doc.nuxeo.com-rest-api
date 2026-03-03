---
title: Sequencers Endpoint
review:
  comment: ''
  date: '2026-03-03'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 625
---

## Get Sequencers

```
GET /management/sequencers
```

### Response

If successful, returns a JSON representation of the configured sequencers.

### Status Codes

- 200 _OK_ - Success.

### Sample

To recompute the video conversions for the documents matching a given query:

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/sequencers
```

```json
{
  "entity-type": "sequencers",
  "entries": [
    {
      "entity-type": "sequencer",
      "name": "default",
      "implementation": "org.nuxeo.ecm.core.uidgen.KeyValueStoreUIDSequencer",
      "keyValues": [
        {
          "key": "audit",
          "value": 13
        }
      ]
    }
  ]
}
```

## Init Sequencer

```
POST /management/sequencers/SEQUENCER_NAME
```

### Path Parameters

| Parameter Name     | Type       | Description         |
| ------------------ | ---------- | ------------------- |
| **SEQUENCER_NAME** | **string** | The sequencer name. |

### Body Parameters

| Parameter Name | Type       | Description                                 | Notes    |
| -------------- | ---------- | ------------------------------------------- | -------- |
| **key**        | **string** | The sequencer key to init                   | Required |
| **value**      | **number** | The sequencer value to init                 | Required |

### Response

If successful, init the sequencer with the given `key` and `value`.

### Status Codes

- 200 _OK_ - Success.
- 400 _Bad Request_ - Given key or value is null

### Sample

To init a specific sequence:

```curl
curl -X POST -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/sequencers/default \
-d 'key=mySequence&value=10'
```

