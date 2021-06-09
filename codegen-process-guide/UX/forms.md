---
layout: page
title: Forms
permalink: /codegen-process-guide/ux/forms
parent: CodeBot UX
grand_parent: CodeBot Guide
nav_order: 5
---

# Input Data with Forms







Binding UI components together.

**State-bound components**, sometimes called "reactive" components, are linked to other components' values by way of "global page state" contained only within the browser.

For example, if the user selects a row in a Videos table, the associated Video object for that row is then held in the global state. A Video Player component may react to the state update, by switching to the selected Video object.

State-bound components are easy to define in your wireframes, using tagged values. Without any programming required (a common theme with CodeBot!), you can link components so that they work together as one cohesive, joined-up UI.


## Defining state-bound components

For example, given a Payments table with columns: Date, amount, status - let's say you want a label to show the current selected amount.

In the Label component, create a tag called bind, and give it the following value (assuming the table is called "Payments Table": 

View Payments History.Payments Table.amount

The three parts are:
1. Wireframe page name
2. Source component name
3. Source domain object's attribute name (if it's a table or some other multi-field component)

The third part isn't always needed, depending on the components being bound together.

The first part (wireframe name) may be omitted if the "target" label and source component are on the same wireframe.

Note that what's actually being bound is the data object being used by the source component. In other words:

Invoices Table -> Invoice (data object) -> Invoice.amount

If a source component only holds one value - e.g. a text field where the user edits the amount - then its state consists only of that one value, not the whole object. So in this case, the third part (attribute name) isn't used.




> **[> Next: Data-bound UI components](data-bound-components)**
