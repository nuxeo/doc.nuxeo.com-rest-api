---
title: Entity Types
review:
    comment: ''
    date: '2019-07-25'
    status: ok
labels:
    - rest-api
    - endpoint
    - multiexcerpt
toc: true
tree_item_index: 300
---

The Nuxeo REST API manages different entity types that define the resource representation managed by the endpoints.

## General Resource Representation

### Single Entity

```json
{
  "entity-type": string,
  "properties": object,
  "contextParameters": object,
  ...
}
```

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
        <td>The entity type name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**properties**</td>
        <td>**object**</td>
        <td>A collection of key-value pairs of properties.</td>
        <td>Optional</td>
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

### List Entity

<pre><code class="json hljs">{
  "entity-type": string,
  "entries": [
    <a href="#general-resource-representation">entity</a>
  ],
  "contextParameters": object,
  ...
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
        <td>The entity type name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**entries[]**</td>
        <td>**list**</td>
        <td>The list of entities.</td>
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

### Paginable Entity

<pre><code class="json hljs">{
  "entity-type": string,
  "entries": [
    <a href="#general-resource-representation">entity</a>
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
  "aggregations": object,
  "quickFilters": [
    {
      "name": string,
      "active": boolean
    }
  ],
  "contextParameters": object,
  ...
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
        <td>The entity type name.</td>
        <td></td>
      </tr>
      <tr>
        <td>**entries[]**</td>
        <td>**list**</td>
        <td>The list of entities.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isPaginable**</td>
        <td>**boolean**</td>
        <td>Whether the entity is paginable. Value: the fixed boolean value `true`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**resultsCount**</td>
        <td>**long**</td>
        <td>The total number of results.</td>
        <td></td>
      </tr>
      <tr>
        <td>**pageSize**</td>
        <td>**long**</td>
        <td>The number of results per page.</td>
        <td></td>
      </tr>
      <tr>
        <td>**maxPageSize**</td>
        <td>**long**</td>
        <td>The max number of results per page.</td>
        <td></td>
      </tr>
      <tr>
        <td>**resultsCountLimit**</td>
        <td>**long**</td>
        <td>The limit of the number of results beyond which the page provider may not be able to compute.</td>
        <td></td>
      </tr>
      <tr>
        <td>**currentPageSize**</td>
        <td>**long**</td>
        <td>The number of entities.</td>
        <td></td>
      </tr>
      <tr>
        <td>**currentPageIndex**</td>
        <td>**long**</td>
        <td>The current page index as a zero-based integer.</td>
        <td></td>
      </tr>
      <tr>
        <td>**currentPageOffset**</td>
        <td>**long**</td>
        <td>The offset of the first element as a zero-based integer.</td>
        <td></td>
      </tr>
      <tr>
        <td>**numberOfPages**</td>
        <td>**long**</td>
        <td>The total number of pages or 0 if unknown.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isPreviousPageAvailable**</td>
        <td>**boolean**</td>
        <td>Whether a previous page is available.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isNextPageAvailable**</td>
        <td>**boolean**</td>
        <td>Whether a next page is available.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isLastPageAvailable**</td>
        <td>**boolean**</td>
        <td>Whether the last page can be reached.</td>
        <td></td>
      </tr>
      <tr>
        <td>**isSortable**</td>
        <td>**boolean**</td>
        <td>Whether the page provider is sortable.</td>
        <td></td>
      </tr>
      <tr>
        <td>**hasError**</td>
        <td>**boolean**</td>
        <td>Whether there was an error while getting the entities.</td>
        <td></td>
      </tr>
      <tr>
        <td>**errorMessage**</td>
        <td>**string**</td>
        <td>The error message.</td>
        <td></td>
      </tr>
      <tr>
        <td>**aggregations**</td>
        <td>**object**</td>
        <td>The aggregates, if any. See "page-provider-aggregates"</td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**quickFilters[]**</td>
        <td>**list**</td>
        <td>The list of quick filters.</td>
        <td></td>
      </tr>
      <tr>
        <td>**quickFilters[].name**</td>
        <td>**string**</td>
        <td>The name of the quick filter.</td>
        <td></td>
      </tr>
      <tr>
        <td>**quickFilters[].active**</td>
        <td>**boolean**</td>
        <td>Whether the quick filter is active.</td>
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
        <td>The entity type name. Value: the fixed string value `exception`.</td>
        <td></td>
      </tr>
      <tr>
        <td>**status**</td>
        <td>**long**</td>
        <td>The error HTTP status code.</td>
        <td></td>
      </tr>
      <tr>
        <td>**message**</td>
        <td>**string**</td>
        <td>A human-readable message about the error.</td>
        <td></td>
      </tr>
      <tr>
        <td>**stacktrace**</td>
        <td>**string**</td>
        <td>The entire stack trace in one string.<!--TODO See error handling page--></td>
        <td>Optional</td>
      </tr>
      <tr>
        <td>**exception**</td>
        <td>**string**</td>
        <td>The entire stack trace wrapped into a nested object.<!-- TODO See error handling page --></td>
        <td>Optional</td>
      </tr>
    </tbody>
  </table>
</div>

<!--
## Enrichment

### Enrichers

### Fetch Properties

### Translated Properties
-->

---
