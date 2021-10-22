---
layout: page
title: Grants
permalink: /codebot-reference/security/grants
parent: Security Reference
grand_parent: CodeBot Reference
nav_order: 2
---

# API Access Control Reference - Grants

Using the built-in RBAC definitions, the following grants are available.

| Grant   | Notes                 |
| ------- | --------------------- |
| add role | The user may assign a role to any user, not including him/herself. |
| add role to self | The user may assign a role to him/herself. This is, of course, quite a special form of grant, as it allows the user to 'bootstrap' their power within the application. However at least one 'superuser' may need this grant, so that new roles may be accessed. |
| create | The user may create a new record in the linked domain. |
| delete any | The user may delete a record belonging to any user in the linked domain. |
| delete own | The user may delete a record belonging to them in the linked domain. |
| read any | The user may read a record belonging to any user in the linked domain. |
| read own | The user may read a record belonging to them in the linked domain. |
| remove role | The user may unassign a role from any user, not including him/herself. |
| remove role from self | The user may unassign a role from him/herself. |
| replace any | The user may replace a record belonging to any user in the linked domain. |
| replace own | The user may replace ('put' a new version of) a record belonging to them in the linked domain. |
| update any | The user may update a record belonging to any user in the linked domain. |
| update own | The user may update ('patch' individual attributes of) a record belonging to them in the linked domain. |

> To clarify, "in the linked domain" means simply the domain class being pointed to by a Dependency arrow.

To assign a grant to a domain permission (the Dependency arrow pointing from an Actor to a domain class), add the grant name (e.g. `read any`) as a UML **constraint** to the Dependency arrow.
