---
layout: page
title: External REST APIs
permalink: /codegen-process-guide/system-integration/external-rest-apis
parent: System Integration
grand_parent: CodeBot Guide
nav_order: 1
---

# Integrating with external REST APIs

Let's say your application needs to call out to some other REST API server - it could be a server maintained by a different team in your organisation, or a third-party REST service running on the internet. We'll generally refer to this as an "external" REST API, in the sense that it's a resource that exists outside your own generated API.

A useful test resource is [JSONPlaceholder](http://jsonplaceholder.typicode.com/), a free online REST API. We'll use it for the example on this page, as JSONPlaceholder provides example APIs that adhere perfectly to established REST conventions.


## How the generated API integrates with external systems

The generated server consists of 3 layers - API Layer, Application Layer and Data Access Layer.

The external API is accessed from the Data Access Layer.

Two types of external REST API are supported:

1. CRUD endpoints
2. Task endpoints

In both cases the API endpoints are defined on a UML Interface. The interface defines the remote operations that can be invoked, along with other details such as the base URL.

Domain classes can then "depend" on this Interface in order to read and write their data (CRUD operations), or invoke *tasks* (such as "send invoice", "issue email reminder").

If you define CRUD operations on the Interface, the generated domain class' application layer will then use these REST operations instead of the default MongoDB operations.

An interface can contain a mix of CRUD and Task endpoints.

> **[> Next: REST API CRUD endpoints](crud-rest-apis)**
