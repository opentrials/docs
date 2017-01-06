## Table of Contents

  - [Overview](#overview)
  - [Search](#search)

## Overview

OpenTrials API manages the schema of our API `database` and search indexes. It also 
exposes the data using RESTful endpoints.

Resources:
- an up-to-date documentation of the API endpoints is available [here](https://api.opentrials.net/v1/docs/).
- more information on the schema of the API `database` in [this section](data-model.md).
- more techical details (stack, how to set up) [here](https://github.com/opentrials/api/blob/master/README.md)

## Search

Our search is powered by [ElasticSearch](https://www.elastic.co/guide/en/elasticsearch/reference/2.3/index.html).

The general format of a `/search` request is:

```
GET /v1/search?q=your_query_here
```

You can pass as value to the `q` parameter any query on indexed attributes that complies with the
[ElasticSearch Query String syntax](https://www.elastic.co/guide/en/elasticsearch/reference/2.3/query-dsl-query-string-query.html).
To see the available attributes for each index check the lists below.

A request on `/search` routes without the `q` parameter will return all results.

Search results are paginated but you can customize the number of results per page.

To see how to navigate between pages and how to construct queries check the [examples section](#examples).

### Trial search

Here is a list of the attributes included in the `Trial` index:

- `identifiers` -  `object`:
    - `{type} (nct, euctr, etc.)`: `string`
- `brief_summary` - `string`
- `source_id` - `string`
- `public_title` - `string`
- `target_sample_size` - `integer`
- `gender` - `string`
- `status` - `string`
- `has_published_results` - `boolean`
- `recruitment_status` - `string`
- `registration_date` - `date`
- `completion_date` - `date`


- `interventions` - `object`:
    - `id` - `string`
    - `name` - `string`
- `intervention` - `string`: maps to `interventions.name`


- `conditions` - `object`:
    - `id` - `string`
    - `name` - `string`
-  `condition` - `string`: maps to `conditions.name`


- `locations` - `object`:
    - `id` - `string`
    - `name` - `string`
    - `type`- `string`
    - `role` - `string`
- `location` - `string`: maps to `locations.name`


- `persons` - `object`: 
    - `id` - `string`
    - `name` - `string`
    - `role` - `string`
- `person` - `string`: maps to `persons.name`


- `organisations` - `object`: 
    - `id` - `string`
    - `name` - `string`
    - `role` - `string`
- `organisation` - `string`: maps to `organisations.name`


- `publications` - `object`: 
    - `id` - `string`
    - `title` - `string`
- `publication` - `string`: maps to `publications.title`


- `documents` - `object`:
    - `id` - `string`
    - `name` - `string`
    - `source_id` - `string`
    - `source_url` - `string`
    - `type` - `string`
    
    - `fda_approval` - `object`:
        - `id` - `string`
        - `action_date` - `date`
        - `notes` - `string`
        - `supplement_number` - [`long`](https://www.elastic.co/guide/en/elasticsearch/reference/current/number.html)
        - `type` - `string`
        - `fda_application` - `object`:
            - `id` - `string`
            - `type` - `string`
            - `drug_name` - `string`
            - `active_ingredients` - `string`
    -  `file` - `object`:
        - `id` - `string`
        - `documentcloud_id` - `string`
        - `source_url` - `string`

#### FDA documents search

Here is a list of the attributes included in the `FDADocuments` index:

- `id` - `string`
- `name` - `string`
- `source_id` - `string`
- `source_url` - `string`
- `type` - `string`

- `fda_approval` - `object`:
    - `id` - `string`
    - `action_date` - `date`
    - `notes` - `string`
    - `supplement_number` - [`long`](https://www.elastic.co/guide/en/elasticsearch/reference/current/number.html)
    - `type` - `string`
    - `fda_application` - `object`:
        - `id` - `string`
        - `type` - `string`
        - `drug_name` - `string`
        - `active_ingredients` - `string`

-  `file` - `object`:
    - `id` - `string`
    - `documentcloud_id` - `string`
    - `source_url` - `string`
    - `pages` - `string` - raw text gathered with optical character recognition from files

- `trial` - `object`:
    - `id` - `string`
    - `public_title` - `string`

#### Examples

* Simple attribute query 

    To get all the `trials` directed at women:
    ```
    GET /v1/search?q=gender:female
    ```
* Navigate to the next page

    ```
    GET /v1/search?q=gender:female&page=2
    ```

* Nested attribute query

    To get all the `trials` that research breast cancer:
    ```
    GET /v1/search?q=conditions.name:breast cancer
    ```
    Notice that we use `conditions.name` to reference the `name` attribute of `conditions`.
    The same syntax applies for any level of nesting in attributes of type `object`.
    
    For ease of use, we also allowed some shorthand queries for common nested attributes (described in the list with `maps to`).
    Therefore you can use the following query to get the same results:

    ```
    GET /v1/search?q=condition:breast cancer
    ```
* Identifiers attribute

    The `identifiers` field is an `object` with names of identifiers as attributes (e.g. `nct`).
    To get all the `trials` with the NCT ID `NCT02887196`:

    ```
    GET /v1/search?q=identifiers.nct:NCT02887196
    ```

* Date attribute query

    To get all the `trials` registered on 26 September 2016: 
    
    ```
    GET /v1/search?q=registration_date:2016-09-26
    ```
* Range queries

    To get all the `trials` registered between 26 September 2016 and 20 October 2016:

    ```
    GET /v1/search?q=registration_date:[2016-09-26 TO 2016-10-11]
    ```
* Multiple attributes

    To get all `trials` directed at women that are ongoing:

    ```
    GET /v1/search?q=gender:female AND status:ongoing
    ```

* Raw text from `File` pages

    To get all `FDADocuments` whose files contain the word "electronic" and its variations e.g.`electronically`

    ```
    GET /v1/search/fda_documents?text=electronic~
    ```

To see the all the possibilities of query check the 
[ElasticSearch documentation](https://www.elastic.co/guide/en/elasticsearch/reference/2.3/query-dsl-query-string-query.html).
