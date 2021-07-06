---
layout: page
title: Domain Modeling
permalink: /codegen-process-guide/domain-modeling/
parent: CodeBot Guide
nav_order: 3
has_children: true
---

# Domain Modeling

CodeBot is essentially a **domain-driven** application generator. That is, it generates working software using a domain model as its primary input. Initially you can start with a relatively "free-form" model with little in the way of details - CodeBot will use sensible defaults and infer as much as it can to fill in the gaps.

As your project progresses, and based on feedback from this early prototype, you'll gradually fill out the domain model with more detail: specific relationship types, multiplicity, business rules, data types etc.



In this guide we're following an example project, a [Location Based Advertising](../lba-project) (LBA) system. Using LBA, advertisers can publish offers (which contain coupons) to the cloud, and a location-aware mobile app can receive and redeem the coupons.

Advertisers pre-purchase blocks of coupons by subscription. When the advertiser has no more coupons available the mobile app will not receive the coupons.

> **[> Next: Draw the domain model as a UML class diagram](class-diagrams)**




