---
layout: page
title: Data-Linked UI Components
permalink: /codegen-process-guide/ux/data-linked-components
parent: CodeBot UX
grand_parent: CodeBot Guide
nav_order: 7
---

# Data-Linked UI Components

Linking components to a remote data source via the REST API.

**Data-linked components** - really, API-linked - get their values from the database. For example, the [Videos table](state-bound-components) discussed in the next page would have been loaded from the Videos database table, via the generated REST API.

Data-linked components are easy to define in your wireframes, using tagged values.

When a page initialises, a "GET" REST request is performed to get the initial data for each domain object in the page. (Or for components such as tables, a GET will return an array of objects).

## Defining data-linked components

The tag to use for data-linked components is domain


## Combining state-bound and data-linked components

Almost all components can be both state-bound and data-linked.

If a component is wired up to be both, it takes its initial value from the database, but can then be updated automatically if a linked component updates. An example of this would be a label that initially shows a value from the database, but can be updated if the user drags a slider component.


> **[> Next: Bind UI components together](state-bound-components)**
