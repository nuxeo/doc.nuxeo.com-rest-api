---
title: User Enrichers
review:
    comment: ''
    date: '2021-10-29'
    status: ok
labels:
    - rest-api
toc: false
---

## userprofile

Get the user profile.

**Example**

```
GET https://NUXEO_SERVER/nuxeo/api/v1/user/USER_ID
enrichers.user: userprofile
```

```json
{
  "entity-type": "user",
  ...
  "contextParameters": {
    "userprofile": {
        "avatar": {
            "data": "https://NUXEO_SERVER/nuxeo/nxfile/default/DOC_ID/userprofile:avatar/avatar.png?changeToken=1-0",
            "digest": "3e2d2f2c73c99fdf20354b43a3def3de",
            "digestAlgorithm": "MD5",
            "encoding": null,
            "length": "10013",
            "mime-type": "image/jpg",
            "name": "avatar.png"
        },
        "birthdate": "1990-02-28T23:00:00.000Z",
        "gender": false,
        "locale": "en_GB",
        "phonenumber": "000 000 000"
    }
}
```

---
