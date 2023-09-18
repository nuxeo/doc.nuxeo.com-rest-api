---
title: Scheduler Endpoint
review:
  comment: ''
  date: '2023-09-18'
  status: ok
labels:
  - http
  - rest-api
toc: true
tree_item_index: 600
---

## Get All Schedules

```
GET /management/schedules
```

### Response

If successful, returns a JSON representation of all schedules.

### Status Codes

- 200 _OK_ - Success.

### Sample

```curl
curl -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/scheduler
```

```json
{
    "entity-type": "schedules",
    "entries": [
        {
            "entity-type": "schedule",
            "id": "aceScheduler",
            "jobFactoryClass": "org.nuxeo.ecm.core.scheduler.DefaultEventJobFactory",
            "eventId": "updateACEStatus",
            "eventCategory": null,
            "cronExpression": "0 0/5 * * * ?",
            "username": null,
            "isEnabled": true,
            "timeZone": null
        },

    ...other schedules...

  ]
}
```

## Stop the scheduler

```
PUT /management/stop
```

### Response

Always 204, this stops the scheduler service cluster-wide. The stops survives a server restart.

### Status Codes

- 204 _NO_CONTENT_

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/scheduler/stop
```

## Start the scheduler

```
PUT /management/start
```

### Response

Always 204, this starts the scheduler service cluster wild.

### Status Codes

- 204 _NO_CONTENT_

### Sample

```curl
curl -XPUT -u Administrator:Administrator \
http://localhost:8080/nuxeo/api/v1/management/scheduler/start
```
