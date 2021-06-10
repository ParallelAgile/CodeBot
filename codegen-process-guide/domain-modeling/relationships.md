---
layout: page
title: Relationships
permalink: /codegen-process-guide/domain-modeling/relationships
parent: Domain Modeling
grand_parent: CodeBot Guide
nav_order: 4
---

# Connect the domain classes using UML relationships

If we return to the "full-on" domain model diagram for a moment, you can see that it includes various types of relationships:

![LBA domain model diagram](../../images/lba/domain-model.png "LBA domain model diagram")

For example:

* Aggregation relationship between `Payment History` and `Payment Transaction` which tells us that a single instance of `Payment History` has 0 or more `Payment Transactions` within them
* Association relationship between `Subscription` and `Coupon Block` which implies that a single `Subscription` has 1 or more `Coupon Block` associated with it. Association creates PK FK relationship in the DB schema between the 2 entities
* Inheritance/Generalization relationship between `Payment Method`, `Wallet Payment` and `Card Payment` where `Payment Method` is the superclass (its attributes and operations) being inherited by subclasses: `Wallet Payment` and `Card Payment`


## Multiplicity

Specifying the multiplicity of class relationships allows you to pin down the details in your domain model. Multiplicity can be specified at the source and target ends of each relationship arrow. The target end generally has more of an effect on the generated code, while the source end (while occasionally used) is more useful for documentation purposes.

If you don’t specify the multiplicity, the default is 0..* (zero to many).

Other value ranges may also be used such as 1..4. This would be interpreted in most cases as "one to many", but may also be put to use for data validation.

If you’re interested in the specifics, the Reference section includes a [full list of relationship types](/CodeBot/codebot-reference/relationship-types) recognised by CodeBot, along with how they're represented in the generated system.

> **[> Next: Domain model naming conventions](naming-conventions)**
