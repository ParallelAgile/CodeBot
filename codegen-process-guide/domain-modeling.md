---
layout: page
title: Domain Modeling
permalink: /codegen-process-guide/domain-modeling
parent: CodeBot Guide
nav_order: 3
---

# Domain Modeling

## Draw the domain model as a UML class diagram

CodeBot handles complex class diagrams including the full set of class relationships (aggregation, composition, associations, dependencies, inheritance) and multiplicity between classes.

Our example project contains various domain classes, all of them linked together with various relationships with multiplicity specified between them and serves to illustrate the basic functions of code generation.


## Specify attributes (example: Store class)

The Store class has a couple of attributes namely: “image” of type “file” (which hints CodeBot to generate appropriate File Upload/Download API endpoints for this attribute), “name” of type “String”, “phone” of type “String” and “website” of type “String”. Other generic attribute types include: int, date, timestamp, time.

The attribute types are generic and not tied to any particular language. CodeBot is intelligent enough to convert generic attribute types to language-specific types. For example: attribute with type “String” gets converted to “varchar” type for relational database schema and the same attribute gets converted to “String” type for the Java client.

![Store domain class](../images/lba/Store.png "Store domain class")
