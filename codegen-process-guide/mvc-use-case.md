---
layout: page
title: The case for full MVC code generation
permalink: /codegen-process-guide/mvc-use-case
---

When software is viewed from a Model View Controller perspective, the generated database access code represents much of the Model part of the code. If you take a simplistic assumption that Model, View and Controller each account for loosely 1/3 of the code, the maximum productivity benefit that’s achievable will likely not exceed this percentage most of the time. Therefore, it’s useful to consider whether similar opportunities for productivity improvement can be achieved by automating the View and Controller portions of the code.

If you can generate code for Models, it’s natural to think about whether View and controller code (i.e., screens and user interface navigation) is also amenable to code generation. A code generator of this category can be driven from a wireframe description of the screen and a state machine that describes UI navigation. These wireframes and state machines can be exported to XML in the same format that CodeBot already uses to ingest a domain model (class diagram). Precedent for developing cross-platform GUI code generators dates back several decades.
