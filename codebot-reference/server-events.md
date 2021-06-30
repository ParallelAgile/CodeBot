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

To define an event, add it to the relevant domain class as an Operation

The following server-side events are created:

| Event         | API endpoint          | Notes              |
| ------------- | --------------------- | ------------------ |
| `onCreate`    | `POST /DomainClass/`  | Called just before an object/record is created |
| `onRead`      | `GET /DomainClass/` | Called after an object/record is read from the DB, and just before it's returned in the HTTP response. When multiple records are returned, onRead is called once for each record. A 'veto' will prevent the whole result-set from being sent. |
| `onReplace`   | `PUT /DomainClass/`   | Called just before an object/record is replaced |
| `onUpdate`    | `PATCH /DomainClass/` | Called just before an object/record is updated. An 'update' operation may involve just one or two of the domain object's fields. |
| `onDelete`    | `DELETE /DomainClass/` | Called just before an object/record is deleted. |

With each of the above "CRUD" functions, if the operation involves multiple records, the event will be called once for each record. A 'veto' will prevent the operation completing for the whole record-set.


# Modifying event data

An important use case for event handlers, besides validating and vetoing input data, is to modify objects that are either being returned to the user, or being written to the database.

To achieve this, each event handler has an input parameter containing the relevant domain object. It's perfectly fine to "mutate" the data in this object... although be aware that where it's *input* data (about to be written to the database), the mutated object must still pass the validation step before being written.


# The 'veto' object

The same 'vetoable' mechanism is used consistently for all event types. So, to veto any event - i.e. prevent it from occurring - return one of the following from the event handler function:

## Return a String containing a 'reason' message

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


## Return a JSON object

To have more control over what's returned from the API, return a JSON object from the event handler, with the following structure:

```JavaScript
(invoice, loggedInUser) => {
    return {
      msg: "All invoices are being rejected today.",
      status: 500
    };
}
```

The message will be returned as a JSON object (as above), with a `500` response.


## No veto

To allow an operation to proceed without being vetoed, simply return nothing (i.e. `undefined`). Returning *any* value besides `undefined` will cause the operation to be aborted.


## Combining veto responses

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

