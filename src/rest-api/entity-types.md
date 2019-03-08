---
title: Entity Types
review:
    comment: ''
    date: '2019-03-07'
    status: ok
labels:
    - rest-api
    - endpoint
    - multiexcerpt
toc: true
tree_item_index: 300
---

The Nuxeo REST API endpoints manages different entity types. An entity type defines the resource representation managed by the endpoints.

## General Resource Representation

### Single Entity

```json
{
  "entity-type": string,
  "properties": {
    (key): string,
  },
  "contextParameters": {
    (key): string,
  },
  ...
}
```

| Property Name               | Value      | Description                                                               |
| --------------------------- | ---------- | ------------------------------------------------------------------------- |
| **entity-type**             | **string** | The entity type name.                                                     |
| **properties**              | **object** | **Optional** A collection of key-value pairs of properties.               |
| **properties.(key)**        | **string** | The property name.                                                        |
| **contextParameters**       | **object** | **Optional** A collection of key-value pairs filled by enabled enrichers. |
| **contextParameters.(key)** | **string** | The enricher name.                                                        |

### List Entity

```json
{
  "entity-type": string,
  "entries": [
    entity
  ],
  "contextParameters": {
    (key): string,
  },
  ...
}
```

| Property Name               | Value      | Description                                                                             |
| --------------------------- | ---------- | --------------------------------------------------------------------------------------- |
| **entity-type**             | **string** | The entity type name.                                                                   |
| **entries[]**               | **list**   | The list of entities.                                                                   |
| **contextParameters**       | **object** | **Optional** A collection of key-value pairs filled by enabled enrichers. |
| **contextParameters.(key)** | **string** | The enricher name.                                                        |

### Paginable Entity

```json
{
  "entity-type": string,
  "entries": [
    entity
  ],
  "isPaginable": boolean,
  "resultsCount", long,
  "pageSize", long,
  "maxPageSize", long,
  "resultsCountLimit", long,
  "currentPageSize": long,
  "currentPageIndex": long,
  "currentPageOffset": long,
  "numberOfPages": long,
  "isPreviousPageAvailable": boolean,
  "isNextPageAvailable": boolean,
  "isLastPageAvailable": boolean,
  "isSortable": boolean,
  "hasError": boolean,
  "errorMessage": boolean,
  "totalSize": long,
  "pageIndex": long,
  "pageCount": long,
  "aggregations": {
    (key): string,
  },
  "quickFilters": [
    {
      "name": string,
      "active": boolean
    }
  ],
  "contextParameters": {
    (key): string,
  },
  ...
}
```

| Property Name               | Value       | Description                                                                               |
| --------------------------- | ----------- | ----------------------------------------------------------------------------------------- |
| **entity-type**             | **string**  | The entity type name.                                                                     |
| **entries[]**               | **list**    | The list of entities.                                                                     |
| **isPaginable**             | **boolean** | Whether the entity is paginable. Value: the fixed boolean value `true`.                   |
| **resultsCount**            | **long**    | The total number of results.                                                              |
| **pageSize**                | **long**    | The number of results per page.                                                           |
| **maxPageSize**             | **long**    | The max number of results per page.                                                       |
| **resultsCountLimit**       | **long**    | The limit of number of results beyond which the page provider may not be able to compute. |
| **currentPageSize**         | **long**    | The number of entities.                                                                   |
| **currentPageIndex**        | **long**    | The current page index as a zero-based integer.                                           |
| **currentPageOffset**       | **long**    | The offset of the first element as a zero-based integer.                                  |
| **numberOfPages**           | **long**    | The total number of pages or 0 if unknown.                                                |
| **isPreviousPageAvailable** | **boolean** | Whether a previous page is available.                                                     |
| **isNextPageAvailable**     | **boolean** | Whether a next page is available.                                                         |
| **isLastPageAvailable**     | **boolean** | Whether the last page can be reached.                                                     |
| **isSortable**              | **boolean** | Whether the page provider is sortable.                                                    |
| **hasError**                | **boolean** | Whether there was an error while getting the entities.                                    |
| **errorMessage**            | **string**  | The error message.                                                                        |
| **aggregations**            | **object**  | **Optional** The aggregates, if any. See "page-provider-aggregates"                       |
| **aggregations.(key)**      | **string**  | The aggregate id.                                                                         |
| **quickFilters[]**          | **list**    | The list of quick filters.                                                                |
| **quickFilters[].name**     | **string**  | The name of the quick filter.                                                             |
| **quickFilters[].active**   | **boolean** | Whether the quick filter is active.                                                       |
| **contextParameters**       | **object** | **Optional** A collection of key-value pairs filled by enabled enrichers. |
| **contextParameters.(key)** | **string** | The enricher name.                                                        |

### Error

The Nuxeo REST API communicates error messages through standard HTTP status codes paired with exception details.

```json
{
  "entity-type": "exception",
  "status": long,
  "message": string,
  "stacktrace": string,
  "exception": object
}
```

| Property Name   | Value      | Description                                                                                     |
| --------------- | ---------- | ----------------------------------------------------------------------------------------------- |
| **entity-type** | **string** | The entity type name. Value: the fixed string value `exception`.                                |
| **status**      | **long**   | The error HTTP status code.                                                                     |
| **message**     | **string** | A human-readable message about the error.                                                       |
| **stacktrace**  | **string** | **Optional** The entire stack trace in one string. TODO See error handling page                 |
| **exception**   | **string** | **Optional** The entire stack trace wrapped into a nested object.  TODO See error handling page |

## Enrichment

### Enrichers

### Fetch Properties

---
