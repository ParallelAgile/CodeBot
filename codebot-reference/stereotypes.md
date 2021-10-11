---
layout: page
title: Stereotypes
permalink: /codebot-reference/stereotypes
parent: CodeBot Reference
nav_order: 4
---

# Reference - Stereotypes

This page contains all the UML stereotypes that CodeBot recognises.

## Stereotypes by Category

The stereotypes are grouped here by their general category.

### Domain Class Stereotypes

| Stereotype | For model elements | Notes               |
| ---------- | ------------------------- | ------------------- |
| ClientSingleton | `Class` |  |
| Public | `Class` | The API will allow any user, including anonymous/not-logged-in users, to read data from a domain class if it has this stereotype.Only 'read' access is allowed, though - anonymous users can't create, modify or delete data. |
| dto | `Class` |  |
| entity | `Class` | Usually a domain class is an 'entity' (data object) by default, so will have its own set of API endpoints, database collection/table etc. This stereotype can be used to either document that it's an entity, or enforce it. |
| testcase | `Class` |  |

### External Api Stereotypes

| Stereotype | For model elements | Notes               |
| ---------- | ------------------------- | ------------------- |
| MongoDB | `Interface` | By default, any domain class is given an 'implied' MongoDB DAO. However, this stereotype can be added to an Interface, so that the model can show domain classes explicitly dependening on it. |
| Rest | `Interface` | Indicates that this Interface models an external REST API. If this stereotype is used, a `url` tagged value should also be added to the Interface. |

### Security Stereotypes

| Stereotype | For model elements | Notes               |
| ---------- | ------------------------- | ------------------- |
| DefaultRole | `Actor` | When a user signs up via /register, any roles with this stereotype are automatically assigned to the new user. |
| FirstUserRole | `Actor` | When the first user in the system signs up via /register, any roles with this stereotype are automatically assigned to the new user. This allows the first user to be given admin permissions. |

### Task Stereotypes

| Stereotype | For model elements | Notes               |
| ---------- | ------------------------- | ------------------- |
| Application | `Operation` | Indicates that this Operation should be placed in the Application Layer of the app server. Required if the Operation represents a custom CRUD function. |
| Task | `Operation` | Indicates that this Operation is a task endpoint. The presence of this stereotype will result in a REST API endpoint, Swagger docs, and default app-layer function (which can be customised or replaced entirely with code). |

