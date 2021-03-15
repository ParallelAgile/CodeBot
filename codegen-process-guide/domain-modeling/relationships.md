---
layout: page
title: Relationships
permalink: /codegen-process-guide/domain-modeling/relationships
parent: Domain Modeling
grand_parent: CodeBot Guide
nav_order: 3
---

# Connect the domain classes using UML relationships

The LBA domain model diagram shows different types of relationships - e.g:

* Aggregation relationship between `PaymentHistory` and `PaymentTransaction` which tells us that a single instance of `PaymentHistory` has 0 or more `PaymentTransactions` within them
* Association relationship between `Subscription` and `CouponBlock` which implies that a single `Subscription` has 1 or more `CouponBlock` associated with it. Association creates PK FK relationship in the DB schema between the 2 entities
* Inheritance/Generalization relationship between `PaymentMethod`, `WalletPayment` and `CardPayment` where `PaymentMethod` is the superclass (its attributes and operations) being inherited by subclasses: `WalletPayment` and `CardPayment`


## Multiplicity

Specifying the multiplicity of class relationships allows you to pin down the details in your domain model. Multiplicity can be specified at the source and target ends of each relationship arrow. The target end generally has more of an effect on the generated code, while the source end (while occasionally used) is more useful for documentation purposes.

If you don’t specify the multiplicity, the default is 0..* (zero to many).

Other value ranges may also be used such as 1..4. This would be interpreted in most cases as "one to many", but may also be put to use for data validation.

If you’re interested in the specifics, the Reference section includes a [full list of relationship types](/CodeBot/codebot-reference/relationship-types) recognised by CodeBot, along with how they're represented in the generated system.

> **[> Next: Domain model naming conventions](naming-conventions)**
