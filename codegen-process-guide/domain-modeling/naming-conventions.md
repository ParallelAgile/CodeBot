---
layout: page
title: Naming Conventions
permalink: /codegen-process-guide/domain-modeling/naming-conventions
parent: Domain Modeling
grand_parent: CodeBot Guide
nav_order: 5
---

# Domain Model Naming Conventions

The main convention that we want to convey here is simply to use "natural language" naming throughout the domain model - in fact, throughout the entire UML model!

The model is positioned at the "business domain" level - which means it's intended as a "human readable" document, and shouldn't delve into design or implementation details.

So, give domain classes names like `Coupon Block` and `Card Payment` instead of `CouponBlock` or `CardPayment`.

Similarly for class attributes, use names like `First name` and `Coupons available` instead of `FirstName`, `first_name`, `couponsAvailable`, `coupons-available` etc.

Natural language naming is also much nicer to work with, as it's easier to read and doesn't look unnecessarily "technical".

When CodeBot is run, it'll automatically convert names to match the code naming conventions of whichever language, markup or platform it's targeting. So `First name` will automatically become `first_name` or `firstName` etc, as needed.


> **[> Next: Generate what you've created so far](generate-api)**
