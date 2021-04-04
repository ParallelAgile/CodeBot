---
layout: page
title: Use Cases
permalink: /codegen-process-guide/ux/use-cases
parent: CodeBot UX
grand_parent: CodeBot Guide
nav_order: 1
---

# Use Cases

Use cases define the system behaviour, from the perspective of an end-user.

Here the LBA project's use cases are defined using Enterprise Architect (EA):

![Defining the use cases in EA](../../images/lba/use-cases-in-ea.png "Defining the use cases in EA")

You can also attribute use cases to specific actors (the "stick men"), which in turn will define the *user roles* - i.e. define who has access to particular domain classes and API functions, based on what their job role requires.

Generally, one use case maps to a particular screen (Login, Register, Pay Invoice etc). Each screen is defined as a wireframe diagram; the easiest way to organise the wireframes is to create each one as a child diagram beneath the relevant use case.

To create a child diagram in EA, right-click on the use case and choose `New Child Diagram`.

The wireframes can also be accessed via the project browser (at the left in the above screenshot), but creating them as sub-diagrams allows you to double-click on a use case to navigate directly to its associated wireframe.

> **[> Next: Design the wireframes](wireframes)**
