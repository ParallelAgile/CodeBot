---
layout: page
title: Generate Your Project
permalink: /codegen-process-guide/domain-modeling/generate-api
parent: Domain Modeling
grand_parent: CodeBot Guide
nav_order: 6
---

# Generate the Database and REST API

Normally you'll expect to do this step quite often. The idea, especially early in the project lifecycle, is to incrementally build a proof-of-concept to gather early feedback from stakeholders. This drives the next version of the domain model, along with more details; the project is then re-generated, tested, and so on. Following this approach, you'll soon have a production-ready system ready for release.


## Run CodeBot!

There are two ways you can run CodeBot:

* Use our add-in for Enterprise Architect
* Export the model to an XMI 2.1 file, and upload it to the [CodeBot Web Console](../getting-started/web-console)


## Use the EA add-in

To use the add-in, simply right-click on the root package in EA, and choose: Specialize > Parallel Agile > Generate.

**The package that you right-click on does make a difference**. Only the selected package (plus any sub-packages) will be generated. So, to be sure you're including everything, make sure you right-click on the root package (usually called `Model`).


## Use the CodeBot Web Console


## Check the results

If you've opted to host the generated application via our cloud service, you can try it out straightaway via the Web Console.

Or alternatively, download the generated zipfile, unzip it into a directory, and explore the generated code. Every "component" in the generated system is set up so it plays nicely with the other parts of the system; so you should be able to just run stuff, and it'll all work together. Each generated component has a README.md file with instructions on setting it up and running it.



CodeBot generates a secure database access REST API with (as a minimum) Create, Read, Update, Delete (CRUD) functions.

There are actually two "update"-type operations:

* **Replace** (replace an entire entity/record - equivalent to an HTTP PUT request)
* **Update** (update individual fields in the entity/record - equivalent to an HTTP PATCH request)

These database access functions can be accessed by screens/web pages generated from wireframes. Linkages between screens and database access functions are specified using UML tagged values.


> **[> Next: CodeBot UX - draw wireframes and generate a React web-app](../UX/)**
