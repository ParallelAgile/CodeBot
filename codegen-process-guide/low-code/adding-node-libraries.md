---
layout: page
title: Adding Node Libraries
permalink: /codegen-process-guide/low-code/adding-node-libraries
parent: Low-Code Capabilities
grand_parent: CodeBot Guide
nav_order: 4
---

# Adding Node Libraries

If you need a Node library that isn't already included in the generated REST API, this can be done as follows.

In the domain class that has an event handler which requires the new library, add a tagged value called either `node dependency` or `node dependencies`:

![Specifying a Node dependency](../../images/low-code/node-dependency.png "Specifying a Node dependency")

CodeBot will then add a `require` statement at the top of the `VideoReviewApi.js` module. The dependency will also be added to `package.json` along with any dependencies specified in other domain classes.

The format in the tagged value is simply:

* `package-name package-version` - i.e. separate the name and version with a space; or:
* `package-name` - if the version isn't specified, "latest" will be used

If you need to add more than one dependency, separate them with commas.

> If the same Node module is specified in several domain classes, be careful that they all use the same version. CodeBot will eliminate duplicates (same name + version), but if it encounters "clashing" versions, it will halt code generation with an error.

--

> **[> Next: Binary file uploads](binary-file-uploads)**
