---
title: Group Fetch Properties
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
toc: false
---

## memberUsers

Add the group member user ids when fetching a group.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/group/GROUP_ID
fetch.group: memberUsers
```
---

## memberGroups

Add the group member group ids when fetching a group.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/group/GROUP_ID
fetch.group: memberGroups
```
---

## parentGroups

Add the group parent group ids when fetching a group.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/group/GROUP_ID
fetch.group: parentGroups
```
---
