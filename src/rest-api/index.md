---
title: REST API
description: This page explains the organization and scope of the existing endpoints and other additional mechanisms which extend the behavior of the API.
review:
    comment: ''
    date: '2019-07-24'
    status: ok
labels:
    - url
    - rest-api
    - university
    - excerpt
    - multi-excerpt
toc: true
notes: Documentation page used by the Marketing team. Check with Marketing before deleting or moving.
---

{{! excerpt}}
The Nuxeo REST API is available on a Nuxeo Server. </br>
All endpoints follow the URL:

```
https://NUXEO_SERVER/nuxeo/api/v1/ENDPOINT
```

This page explains the organization and scope of the existing endpoints and other additional mechanisms which extend the behavior of the API.
{{! /excerpt}}

{{! multiexcerpt name='RestAPIIntroduction'}}

{{#> callout type='info' heading='Nuxeo University'}}
Watch the related [course on Nuxeo University](https://university.nuxeo.com/learn/public/course/view/elearning/66/rest-api).
![]({{file name='university-restapi.png' page='nxdoc/university'}} ?w=450,border=true)
{{/callout}}

## Example

Get the `default-domain` document by its path:

```bash
curl -u Administrator:Administrator  https://nightly.nuxeo.com/nuxeo/api/v1/path/default-domain
```

## Scope and Concepts

The Nuxeo REST API is the best way to remotely integrate portals, workflow engines, Enterprise Service Bus (ESBs) and custom applications written in JavaScript, Ruby, etc, with a Nuxeo Server.

See [Endpoints]({{page page='endpoints'}}) for more detailed information on the provided endpoints and how to contribute your own.

## Additional Features

The Nuxeo REST API offers several additional features compared to a standard REST API:

- The use of [Content enrichers]({{page space='nxdoc' page='content-enrichers'}}) in request headers which allow you to request more information with the returned resources (for example, receiving all of a document's children in addition to the document itself).
- The use of [Web Adapters]({{page space='nxdoc' page='web-adapters'}}) which transform the resources returned (for example, getting all the tasks of a document, or its related documents).
- The ability to pipe command calls on a resource.

## Learn More

- Visit the [Nuxeo API Playground](http://nuxeo.github.io/api-playground/) to experiment with different endpoints on your Nuxeo instance. You can read the [Nuxeo API Playground]({{page space='nxdoc' page='nuxeo-api-playground'}}) documentation for more information on how to use it.
- Discover the Nuxeo Platform and its features through its [REST API]({{page space='nxdoc' page='discover-nuxeo-platform-apis'}}).
- Check out some [consecutive cURL calls to get familiar with the resource/command variations of the API]({{page space='nxdoc' page='using-curl'}})

## Available Client SDKs
<!--
// TODO
-->
We provide several client SDKs to make it even easier to use the API integrated with the Nuxeo Platform:
- [Java client]({{page space='nxdoc' page='java-client'}})
- [JavaScript client]({{page space='nxdoc' page='javascript-client'}})
- [iOS client]({{page space='nxdoc' page='ios-client'}})
- [PHP client]({{page space='nxdoc' page='php-automation-client'}}) (partial implementation)
- [DART client](https://github.com/nelsonsilva/nuxeo-dart-client)
- [.NET Client]({{page space='nxdoc' page='net-client'}})
{{! /multiexcerpt}}
