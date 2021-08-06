---
layout: page
title: REST API Custom Event Handlers
permalink: /codegen-process-guide/low-code/event-handlers
parent: Low-Code Capabilities
grand_parent: CodeBot Guide
nav_order: 1
---

# REST API Custom Event Handlers

Event handlers are the chief mechanism that makes CodeBot a full-fledged Low-Code platform and not just No-Code.

Event handlers are designed to encourage domain-driven development, to a quite fundamental level. Each event handler is a custom JavaScript function linked to a particular domain class and event (such as "on create", "on login" or "on update"). As a result, each function is an encapsulation of some discrete element of business domain behaviour, e.g. enforces a business rule or a data validation step.

All event handlers run server-side, so can serve as an "enforcer" of business rules.

> If you need custom code to run client-side (e.g. in generated React pages), consider using [state behaviour functions](ui-behavior-functions).


# Writing an event handler

Each event handler consists of a JavaScript block, which you write in the "code" section of a UML class Operation (method). This code is then injected into the generated REST API code, inside a JavaScript ES6-style arrow function.

For example, given a domain class called Offer, the following `on create` event handler (your code)...

```JavaScript
if (offer.amount == 0) return "Offer amount must be greater than 0"
```

... will be generated as:

```JavaScript
const onCreate = async (offer, loggedInUser, directive) => {
    if (offer.amount == 0) return "Offer amount must be greater than 0"
}
```

(We explain all the above in this page and the Reference Guide).



# Example event handler uses

Event handlers have a number of uses, the main ones being:

* veto an event
* perform data validation
* modify event data
* check that a user is allowed to access (or modify) the data they're requesting

To define an event, add it to the relevant domain class as an Operation

Let's expand on the above list of event handler uses.

## Veto an event

An example of a veto event could be if a user has been banned for some amount of time, so their username is on a "banned" list. So their login attempt can be vetoed.

In the `onLogin` event handler:

```
if (bannedUsernames.contains(account.username)) {
    return "You are currently barred from logging in; please email us if you believe this is in error."
}
```

The `bannedUsernames` variable would need to be initialised and loaded from somewhere. This could go in the `_init` event handler, which allows you to initialise variables at the Domain API "module scope" - i.e. the variables can then be accessed by other code in the same module, such as our `onLogin` function.

You'll find more details about event vetoing in the [Reference section]((../../codebot-reference/server-events)).


## No veto

To allow an operation to proceed without being vetoed, simply return nothing (i.e. `undefined`). Returning *any* value besides `undefined` will cause the operation to be vetoed.

A specialised form of data vetoing is, of course, data validation.


## Perform data validation

The event handler can perform data validation on incoming "create" or "update" domain objects.

e.g. if a new user is signing up, in the `onRegister` event handler:

```
if (account.password.length < 8)) {
    return "Password is too short"
}
```


## Modify event data

An important use case for event handlers, besides validating and vetoing input data, is to modify objects that are either being returned to the user, or being written to the database.

For example, you may want to change or remove a field in the response object, or add new "derived" fields.

To achieve this, each event handler has an input parameter containing the relevant domain object. It's perfectly fine to "mutate" the data in this object... although be aware that where it's *input* data (about to be written to the database), the mutated object must still pass the validation step before being written.


## check that a user is allowed to access (or modify) the data they're requesting

This use case is the basis for [Attribute-Based Access Control](../security/abac) (ABAC), which we cover in the linked page.



## Custom Node dependencies

Finally, if you need to access a Node library that isn't already included in the generated REST API, this can be done as follows.

In the domain class that has an event handler which requires the new library, add a tagged value called either `node dependency` or `node dependencies`:

![Specifying a Node dependency](../../images/low-code/node-dependency.png "Specifying a Node dependency")

CodeBot will then add a `require` statement at the top of the `VideoReviewApi.js` module. The dependency will also be added to `package.json` along with any dependencies specified in other domain classes.

The format in the tagged value is simply:

* `package-name package-version` - i.e. separate the name and version with a space; or:
* `package-name` - if the version isn't specified, "latest" will be used

If you need to add more than one dependency, separate them with commas.

> If the same Node module is specified in several domain classes, be careful that they all use the same version. CodeBot will eliminate duplicates (same name + version), but if it encounters "clashing" versions, it will halt code generation with an error.


## Event handlers are domain driven

The idea behind event handlers is that they're domain driven - essentially a captured business rule that's organised as part of the domain model itself, right on the relevant domain class.

As such, they adhere to many of the original ideas behind Domain Driven Design, in that the domain model - as it evolves with increasing amounts of business understanding and detail - captures both the data structure and the business rules, in the form of strict behaviour - validation, filtering etc.

With this in mind, we recommend that event handler code is kept "framework-independent" as far as possible. So the same code could be injected into the generated Express REST API (as it currently is), or into some other architectural component, e.g. a database of executable business rules... or a suite of automated acceptance tests, Model Checking scripts, etc.

With that said, we recognise that event handlers may also be a kind of "Get out of jail free" card, allowing edge cases or vital functionality to be implemented in the generated API.


## Event handlers are asynchronous

Each event handler can return nothing at all (`undefined`), a simple object, or - optionally - a JavaScript promise. The latter allows event handlers to run asynchronous tasks, such as sending an email, parsing a JSON document, or running ad-hoc database queries.

Please note, however, that the API server waits for the function to complete before returning its response to the caller. So for a *very* lengthy process (more than a few seconds, say) you might instead want to use the event handler to trigger a separate process, and allow the client to monitor its completion status.



[Server-side event handler reference](../../codebot-reference/server-events)


> **[> Next: Custom UI state behavior functions](ui-behavior-functions)**
