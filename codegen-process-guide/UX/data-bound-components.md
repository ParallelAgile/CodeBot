---
layout: page
title: Data-Bound UI Components
permalink: /codegen-process-guide/ux/data-bound-components
parent: CodeBot UX
grand_parent: CodeBot Guide
nav_order: 7
---

# Data-Bound UI Components

Binding components to a remote data source via the REST API.

**Data-bound components** - really, API-bound - get their values from the database. For example, the [aforementioned](state-bound-components) Videos table would have been loaded from the Videos database table, via the generated REST API.

Data-bound components are easy to define in your wireframes, using tagged values.

When a page initialises, a "GET" REST request is performed to get the initial data for each domain object in the page. (Or for components such as tables, a GET will return an array of objects).

## Defining data-bound components

The tag to use for data-bound components is domain


## Combining state-bound and data-bound components

Almost all components can be both state-bound and data-bound.

If a component is wired up to be both, it takes its initial value from the database, but can then be updated automatically if a linked component updates. An example of this would be a label that initially shows a value from the database, but can be updated if the user drags a slider component.


> **[> Next: Bind UI components together](state-bound-components)**
