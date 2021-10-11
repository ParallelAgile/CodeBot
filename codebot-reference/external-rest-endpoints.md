---
layout: page
title: Tailoring External REST Endpoints
permalink: /codebot-reference/external-rest-endpoints
parent: CodeBot Reference
nav_order: 7
---

# Reference - Tailoring External REST Endpoints

> Also see the [External REST APIs](../../codegen-process-guide/system-integration/crud-rest-apis) tutorial.

To tailor an external REST endpoint, create an Operation on the API Interface. The Operation should be named to match the REST endpoint you're tailoring, as follows:

| Operation name | HTTP method |
| -------------- | ----------- |
| `create`       | `POST`      |
| `count` *      | `GET`       |
| `count all` *  | `GET`       |
| `read one`     | `GET`       |
| `find one`     | `GET`       |
| `read many`    | `GET`       |
| `delete one`   | `DELETE`    |
| `delete many`  | `DELETE`    |
| `replace one`  | `PUT`       |
| `modify one`   | `PATCH`     |

> * The default implementation for `count` and `count all` is to first retrieve all matching records via a `GET` call, and count the number of records in the result-set. This is intended for proof-of-concepts only! For production systems, we recommend that these two endpoints are either replaced with a more optimal custom version, or stubbed-out so they can't be called accidentally.

For each Operation, the following tagged values can be used:

| Tag name          | Notes |
| ------------- | ----------- |
| `path`      | Appends the value to the base URL. `/` characters aren't needed at the start or end of the path (or base URL), these will be added automatically. |
| `url`       | Replaces the entire base URL with the value. |
| `method`    | Use the specified HTTP method instead of the default. Allowed values are: GET, POST, PUT, PATCH, DELETE, HEAD, OPTIONS. |

## Further customisation

If the above configuration doesn't cover your particular case, it's also possible to use the "nuclear option" and entirely replace the generated "endpoint caller" function. To do this, add a block of JavaScript code to the "code" tab in the Operation properties.

This code will be injected into an async function in the generated REST DAO.

The following local variables are available in the injected function (in addition to any in-scope variables or functions in the DAO module):


| Operation name | Variable name | Notes |
| -------------- | ----------- | ------- |
| `create`       | `items`     | Array containing one or more domain entities (JSON objects) being created. |
| `create`       | `onFailure` | Callback function; call this if an error occurred such as a connection failure or status 500 response. |
| `create`       | `onCreateError` | Callback function; call this if a REST error occurred such as validation error (status 400 response). |
| `create`       | `onSuccess` | Callback function; call this with a JSON object indicating the operation succeeded. |
| `count`        | `query`     | JSON object representing the query, e.g. `{ name: "Smith" }` |
| `count`        | `onFailure, onQueryError, onSuccess`     | As with `create`, above |
| `count all`    | `onFailure, onQueryError, onSuccess`     | As with `create`, above |
| `read one`     | `id`         | String type; the ID of the item to look up.  |
| `read one`     | `onNotFound` | Callback function; call this with a JSON object indicating the ID wasn't found. |
| `read one`     | `onFailure, onQueryError, onSuccess`     | As with `create`, above  |
| `find one`     | `query`      | JSON object representing the query - same format and expected search behaviour as with `count`, above |
| `find one`     | `options`    | JSON object containing search options |
| `find one`     | `onFailure, onQueryError, onNotFound, onSuccess` | As above... |
| `read many`    | `query`      | JSON object representing the query. |
| `read many`    | `options, onFailure, onQueryError, onNotFound, onSuccess` | As above... |
| `delete one`   | `id`         | String type; the unique ID of the item to delete. |
| `delete one`   | `onFailure, onQueryError, onNotFound, onSuccess` | As above... |
| `delete many`  | `query`     | JSON object representing the search query; all matching items should be deleted.  |
| `delete many`  | `onFailure, onQueryError, onSuccess`     | As above... |
| `replace one`  | `id`        | String type; the ID of the item to replace. |
| `replace one`  | `data`      | JSON object containing the entire record that will replace the existing one. |
| `replace one`  | `onFailure, onQueryError, onSuccess` | As above... |
| `modify one`   | `id`     | String type; the ID of the item to patch. |
| `modify one`   | `data`     | JSON object containing the individual fields that will be patched into the matching record. |

Rather than coding the custom methods directly into Enterprise Architect or MagicDraw etc, we strongly recommend that you:

1. Add a comment line into the code block for each custom Operation
2. Generate the application
3. Locate and edit the custom functions in each respective DAO module
4. Run and test the customised API, via an IDE such as VS Code - set breakpoints in the code to see exactly what's happening
5. Copy & paste the code blocks back into the domain model
