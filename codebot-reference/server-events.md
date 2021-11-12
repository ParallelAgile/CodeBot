---
layout: page
title: Server-Side Events
permalink: /codebot-reference/server-events
parent: CodeBot Reference
nav_order: 5
---

# Reference - Server-Side Events

Server events are triggered in the generated REST API server. For each of these, you can write an event handler in JavaScript - this custom function can:

* perform validation on incoming "create" or "update" domain objects
* veto the event, e.g. prevent a login occurring
* modify the event data, e.g. change or remove a field in the response object, or add new "derived" fields
* check that a user is [allowed to access](../codegen-process-guide/security/abac) (or modify) the data they're requesting
* log the event on a message queue
* do pretty much anything else you need it to

To define an event, add it to the relevant domain class as an Operation. The operation name may follow the naming convention described near the end of this page.

## Where the event handlers are placed in the generated code

Currently these event handlers are treated as "API layer" events, and so are placed in the respective domain-class API module (e.g. "AccountApi.js").
However, please note that they'll soon be moved to the application layer, as they're really just another place to define and enforce application logic/business rules (validation, etc).
This shouldn't affect how they're written, but it does mean that they'll also be available in the separate "Application" codebase - see the `application` folder in the generated zipfile.

## "Request-triggered" event types

The majority of server events are triggered by an incoming request.

For each such request, the following types of event are triggered, and can be "caught" by an event handler:

| Event type    | When called...        | Example uses      |
| ------------- | --------------------- | ----------------- |
| `on ...`     | Just before the requested operation happens. This allows the event itself to be vetoed before it happens. | Rules-based data validation that goes beyond the built-in attribute type checking; e.g. validate an incoming 'create' object, and veto the request if the object validation fails. |
| `on ... success` | Just after an operation has successfully completed, before the response is sent back to the client. | Modify the response object in some way, e.g. rename, add or remove fields; additional logging; post the result to a message queue. |
| `on ... failure` | Just after an operation failed in some way, before the response is sent back to the client. | Modify the error message; additional error logging; trigger a "rainy day" execution flow in the case of a particular error. |

## "Request-triggered" events

The following server-side events are triggered by incoming API requests:

| API endpoint,<br>Events | Notes              |
| ------------- | ------------------ |
| **POST /count:**<br> `on count`<br>`on count success`<br>`on count failure`<br> | Returns the number of items in this domain that match the query provided in the request. |
| **POST :**<br> `on create`<br>`on create success`<br>`on create failure`<br> | Creates a new domain object/record. |
| **DELETE :**<br> `on delete file`<br>`on delete file success`<br>`on delete file failure`<br> | Deletes a file that belongs to a domain object and attribute. |
| **DELETE :**<br> `on delete many`<br>`on delete many success`<br>`on delete many failure`<br> | Deletes any items in this domain that match the query provided in the request. |
| **DELETE :**<br> `on delete one`<br>`on delete one success`<br>`on delete one failure`<br> | Deletes a single item in this domain if it matches the ID provided in the request. |
| **GET :**<br> `on download file`<br>`on download file success`<br>`on download file failure`<br> | Downloads a file that belongs to a domain object and attribute. |
| **POST /find:**<br> `on find many`<br>`on find many success`<br>`on find many failure`<br> | Returns all items in this domain that match the query provided in the request body. |
| **GET :**<br> `on find one`<br>`on find one success`<br>`on find one failure`<br> | Returns up to 1 item in this domain that matches the query provided in the request body. |
| **GET :**<br> `on get many`<br>`on get many success`<br>`on get many failure`<br> | Returns all items in this domain that match the query provided in the request query parameters. When multiple records are returned, the event handler is called once for each record. A 'veto' will prevent the whole result-set from being sent. |
| **POST :**<br> `on login`<br>`on login success`<br>`on login failure`<br> | Authenticates the user via username/password in the request body. |
| **GET :**<br> `on read one`<br>`on read one success`<br>`on read one failure`<br> | Returns up to 1 item in this domain that matches the ID provided in the request path. |
| **POST :**<br> `on register`<br>`on register success`<br>`on register failure`<br> | Creates a new user record, or 'identity'. The password is hashed before being written to the database. |
| **PUT :**<br> `on replace`<br>`on replace success`<br>`on replace failure`<br> | Replaces the whole record that matches the ID provided in the request path, given a JSON object in the request body. The JSON object doesn't need to include the ID itself. |
| **PUT :**<br> `on replace file`<br>`on replace file success`<br>`on replace file failure`<br> | Uploads a replacement file that belongs to a domain object and attribute. |
| **PATCH :**<br> `on update`<br>`on update success`<br>`on update failure`<br> | Updates (patches) individual fields in the record that matches the ID provided in the request path. The fields to patch are provided as a JSON object in the request body. |
| **POST :**<br> `on upload file`<br>`on upload file success`<br>`on upload file failure`<br> | Uploads a new file (binary or otherwise) that belongs to a domain object and attribute. |
|  **/task/....** <br>`on (task)`<br>`on (task) success`<br>`on (task) failure`<br> | Given a custom task-based API endpoint, these server events are triggered and can be handled just like the built-in CRUD API events. |

## Other server events

The above events are triggered by incoming API requests. Additionally, a small number of "non-request" server events can be listened for:

| Event         | Notes              |
| ------------- | ------------------ |
| `on start`    | Called once when the domain API starts up. This may be used, for example, to call the associated DAO to create "bootstrap" data. |
| `_init`       | Allows variables or resources to be initialised at the "module scope" of the domain API. `_init` code shouldn't be wrapped in an arrow function; instead the block of code is placed and run directly at the top of the module. This allows variables to be declared that can then be accessed by other functions in the same module. Use with care! |

If the operation involves multiple records, the event will be called once for each record (except for `on read many`, which is called once with the complete record-set). A 'veto' will prevent the operation completing for the whole record-set.

## Naming

In the above tables, we've used "lower sentence case" for each event/Operation name. We recommend this convention is used in your own domain model, as it retains a "business specification" feel to the domain model - plus it's just nicer to read.

In the JavaScript-based Express REST API, each Operation name is morphed into "lowerCamelCase".

## Function arguments

Although some input arguments aren't relevant for all events, we've tried to keep the argument ordering consistent:

```JavaScript
async (entityName, loggedInUser, directive) => {}
```

where `entityName` is the domain class name in lowerCamelCase, e.g. `account`, `hotelReview` or `badDriverReport`.

* `(entityName)` is the data object, either incoming (for write operations such as `on create` and `on replace`), or outgoing (`on read` etc).
* `loggedInUser` is, as you'd expect, the data object loaded from the DB for the logged-in user identified by their JWT token.
* `directive` allows you to have some additional control over the response. The `directive` object is placed directly in the response JSON, so you can add custom fields which your own client code can then read.

`directive` is useful particularly for UX, to [direct the user to a different page](../codegen-process-guide/ux/navigation).

There are some exceptions to the above function arguments, as follows.

### `onReadMany` function arguments

The `onReadMany` function arguments are as follows:

```JavaScript
async (data, loggedInUser, directive) => {}
```

* `data` is an object containing a single field called `items` - this being an array of all the entity items that have been read.
* `loggedInUser` - as above.
* `directive` - as above.

This structure enables the array to be more easily filtered or mapped-over. Just ensure the `data.items` reference is updated with the new array.

For example:

```JavaScript
data.items = data.items.filter(review => review.rating == 5);
```

### `onDeleteMany` function arguments

The `onDeleteMany` function arguments are as follows:

```JavaScript
async (query, loggedInUser, directive) => {}
```

Because this event handler is run prior to the delete operation taking place, and no "read" is performed first, no "data" object or array is passed in.

Instead, the first arg is instead called `query`, and contains a JavaScript object containing the attribute names and values that will be used in the delete operation.

> If you did want to load the same records to check them before deletion, you could do this in the `onDeleteMany` event handler, by calling the relevant DAO function directly.


## The 'veto' object

The same 'vetoable' mechanism is used consistently for all event types. So, to veto any event - i.e. prevent it from occurring - return one of the following from the event handler function:

### Return a String containing a 'reason' message

```JavaScript
(invoice, loggedInUser) => {
    return "All invoices are being rejected today.";
}
```

The message will be returned from the API, as a JSON object:

```JSON
{
  "message": "All invoices are being rejected today."
}
```

The message field can either be a string (as above) or an array of strings, if multiple records were vetoed (see "Combining veto responses", below).

The response will have a `400` status code.


### Return a JSON object

To have more control over the veto response, return a JSON object from the event handler, with the following structure:

```JavaScript
(invoice, loggedInUser) => {
    return {
      msg: "All invoices are being rejected today.",
      status: 500
    };
}
```

The message will be returned as a JSON object (as in the previous example), with a `500` response.

### Combining veto responses

In the case where an operation involves multiple records (therefore potentially multiple vetoes), the vetoes will be filtered to remove duplicates, then returned in a string array:

```JSON
{
  "message": [
    "First rejection reason",
    "Second rejection reason"
  ]
}
```

Additionally, the first occurring status code will be used, or the default `400` if none was specified.
