---
layout: page
title: Choosing a Database
permalink: /articles/choosing-a-database
parent: Articles
nav_order: 2
---

# Choosing a Database

At the time of writing, CodeBot generates a REST API that connects to a back-end MongoDB database, i.e. "NoSQL". We're in the process of adding support for RDBMS's including Oracle, MySQL/MariaDB, PostgreSQL and SQL Server.

An overriding goal is that the middleware REST API shouldn't be affected by the choice of database. So, *functionally* it makes no difference which database you go with. The choice is effectively an architectural one, with the storage and retrieval details hidden away by the middleware API.

So any client software is shielded from the differences and doesn't need to be rewritten if a different database is swapped in.

This allows something as fundamental as the overall architecture to be "evolved" during development (particularly during the project's proof-of-concept phase), with minimal impact on the codebase.

Of course, there are major differences in features and capabilities between a NoSQL database such as Mongo and a relational database such as Oracle. In particular, with an RDBMS, different tables are usually linked via foreign key relationships, allowing relationships to be traversed, and cascading deletes to happen automatically. Conversely, in MongoDB the equivalent collections are isolated; there's little to no support for maintaining relationships between collections. This is, of course, by design, and it's central to the idea behind MongoDB. The trade-off is that (in theory) Mongo can be faster to create, update and retrieve records.

Another difference is that Mongo supports hierarchical data structures, in the form of nested JSON objects and arrays. If you delete the parent record, its nested data is also naturally deleted, as they're part of the same document. Other databases generally don't have this feature. (Postgres does allow storage of JSON data, but doesn't support "native" querying and indexing of the nested objects - in other words, each JSON record is more like an opaque "blob" of data until it's retrieved).

CodeBot handles these differences by "filling in" any missing features at the middleware API level; or by using an equivalent "database-native" feature where possible. For example, with MongoDB the generated API maintains "foreign-key-like" relationships between collections. CodeBot also generates indexes so that lookup of records in child or parent collections is still relatively fast. We're also currently adding complex query support, so that an API client can retrieve records from a parent collection and related child collections in a single query.

(One implication of this is that CodeBot provides RDBMS-like lookup & table traversal capabilities for MongoDB, via the middleware layer. We're pretty excited about that!)

To "simulate" the effect of nested JSON objects, the RDBMS-backed APIs maintain a different table for each sub-object, linked to their parent container via a foreign key. A cascading delete is created, so that if the parent container row is deleted, so are any "contained" rows in child tables.

This implies a strong relationship; indeed, this structure is modeled in the UML domain model as "composition" - meaning that it wouldn't make sense for the child object to exist without the parent (e.g. a list of special offers belonging to a product. If the product is deleted, so are the special offers).

Implementing the equivalent features at the API level provides many advantages. As you would expect, though, the database-native equivalent will always be the better option: more performant and more "transactional", in the sense that the database itself can maintain data integrity closer to the data.

So, switching databases while developing a proof-of-concept allows you to change your mind while the domain model is still evolving.

Ultimately, because the consistent API offers the same feature-set regardless of which database you choose, the choice of database comes down to the *non-functional requirements*: e.g. does your product favour write speed over complex queries spanning multiple tables?

With CodeBot, it's easy to run performance tests with different storage & retrieval scenarios, across different databases, with a consistent API. Simply run the tests first with the Mongo-backed REST API, then shut it down, start up the Oracle-backed REST API, and re-run the exact same tests.

In this way, you can be fairly "scientific" about exactly which database will best suit your project.
