---
layout: page
title: Server-Side Events
permalink: /codebot-reference/server-side-events
parent: CodeBot Reference
nav_order: 4
---

# Reference - Server-Side Events

Server-side events are triggered in the generated REST API server. For each of these, you can write an event handler in JavaScript - this custom function can:

* perform validation on incoming "create" or "update" domain objects
* veto the event, e.g. prevent a login occurring
* modify the event data, e.g. change or remove a field in the response object, or add new "derived" fields
* check that a user is [allowed to access](../codegen-process-guide/security/abac) (or modify) the data they're requesting

To define an event, add it to the relevant domain class as an Operation.

The following server-side events are created:

| Event         | API endpoint             | Notes              |
| ------------- | ------------------------ | ------------------ |
| `on create`    | `POST /DomainClass/`     | Called just before an object/record is created |
| `on create success` | `POST /DomainClass/` | Called just after a record is created |
| `on file upload success` | `POST /DomainClass/attribute_name/` | Called just after a binary file (PNG, MPEG etc) is uploaded and stored |
| `on read`      | `GET /DomainClass/`      | Called after an object/record is read from the DB, and just before it's returned in the HTTP response. When multiple records are returned, onRead is called once for each record. A 'veto' will prevent the whole result-set from being sent. |
| `on read many`      | `GET /DomainClass/`      | Called after a batch of objects/records are read from the DB, and just before they're returned in the HTTP response. Unlike `on read`, `on read many` is called once with an array of all the records that were read. This event handler can be used, for example, to filter the result-set before it's returned. |
| `on replace`   | `PUT /DomainClass/`      | Called just before an object/record is replaced |
| `on update`    | `PATCH /DomainClass/`    | Called just before an object/record is updated. An 'update' operation may involve just one or two of the domain object's fields. |
| `on delete`    | `DELETE /DomainClass/`   | Called just before an object/record is deleted. |
| `on start`     | | Called once when the domain API starts up. This may be used, for example, to call the associated DAO to create "bootstrap" data. |
| `_init`    | | Allows variables or resources to be initialised at the "module scope" of the domain API. `_init` code shouldn't be wrapped in an arrow function; instead the block of code is placed and run directly at the top of the module. This allows variables to be declared that can then be accessed by other functions in the same module. Use with care! |

If the operation involves multiple records, the event will be called once for each record (except for `on read many`, which is called once with the complete record-set). A 'veto' will prevent the operation completing for the whole record-set.

## Naming

In the above table, we've used "lower sentence case" for each event/Operation name. We recommend this convention is used in your own domain model, as it retains a "business specification" feel to the domain model - plus it's just nicer to read.

In the JavaScript-based Express REST API, each Operation name is morphed into "lowerCamelCase".

## Function arguments

Although some input arguments aren't relevant for all events, we've tried to keep the argument ordering consistent:

```JavaScript
(entityName, loggedInUser, directive) => {}
```

* `entityName` is the data object, either incoming (for write operations such as `on create` and `on replace`), or outgoing (`on read` etc).
* `loggedInUser` is, as you'd expect, the data object loaded from the DB for the logged-in user identified by their JWT token.
* `directive` allows you to have some additional control over the response. The `directive` object is placed directly in the response JSON, so you can add custom fields which your own client code can then read.

`directive` is useful particularly for UX, to [direct the user to a different page](../codegen-process-guide/ux/navigation).


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

