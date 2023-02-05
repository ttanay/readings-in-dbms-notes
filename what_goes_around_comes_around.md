# What goes around comes around

Author(s): Joe Hellerstein, Michael Stonebraker
Created: January 30, 2023 12:21 AM
Source: https://lapti.ct.utfpr.edu.br/MateriaisCursos/DataScience/papers/WhatGoesAroundComesAround-SH05.pdf
Tags: Databases, History

CODASYL failed because of its complexity

Eras:

1. Hierarchical: 60s, 70s
2. Network(CODASYL): 70s
3. Relational: 70s and 80s
4. Entity-Relationship: 70s
5. Extended Relational: 80s
6. Semantic: 70s and 80s
7. Object-oriented: 80s and 90s
8. Object-relational: 80s and 90s
9. Semi-structured(XML): 90s to present

Eg:

1. Supplier
2. Part
3. Supply

## IMS

Record types are arranges in a tree! Parent record type for all record types except root.

Similar to graph databases?

Cons:

1. Information is repeated
    1. Inconsistency
2. Existence depends on parents
    1. Corner cases missing. No standalone NULLs

HSK(Hierarchical Sequence Key) identifies a node in the hierarchy/tree
Physical plan not separated from the logical plan
Developer needs to deal with implementation details

Storage options:

1. stored seuqentially
    1. Inserts will be a problem. Good for batch proessing(old-master, new-master)
2. B-Tree
3. Hashed
    1. Can’t order on hashed records(ORDER BY hash)

Storage tightly coupled with intended use. ← Reminiscent of modern special-purpose storage? Eg: Graph/Feature stores
What about no one size fits all?
Phyical data independence → Allows evolution
DL/I has some logical data independence.
Logical data independence → Allow application/data evolution
“fused” structure is essentially denormalized.
Does seem like a subset of relational databases.
The Graphite metrics series seems to be a similar data model!
https://graphite.readthedocs.io/en/latest/feeding-carbon.html#step-1-plan-a-naming-hierarchy

## CODASYL

Data organized in a network rather than a tree
1-N relationship as in relational model
1-N ⇒ 1-0 also possible
CODASYL sets are 2-way only
It is a record-at-a-time language ⇒ Navigation one set at a time. How does this compare to graph traversal in graph database queries?
No physical and logical data independence
Queries are tied to the current state of the naigational pointer ⇒ stateful queries
Large network is hard to load. IMS database can be bulk-loaded ⇒ Complicates crash recovery

Cons:

1. complex
2. record-at-a-time hard to optimize(in th QL)
3. less data independence
4. not flexible enpugh

## Relational Model

Goal: Data Independence

1. Store data in simple DS
2. Se-at-a-time DML
3. No talk physical

See QUEL

Q: how are graph data models different from network models(codasyl)

## Entity-Relationship

Studied this in college for schema design
Why couldn’t the sysadmins understand the functional dependencies?
Chen papers used to for initial E-R schema. Can be converted easily to 3NF.
TODO: functional dependencies have a formal definition in database theory. PK/FK/Unique/CHECK  constraints are examples of functional dependencies.

## R++

80s had papers that modified relational model for special cases. Eg: Time. Look at the paper to figure out how that would help the relational mode.

Modifications:

1. Set-value attribute(Enums?)
2. FK pointers: Allowed joins
3. Generalization/Inheritance: Q: Does this exist in modern SQL?
    1. Tuples as a data type were less than almost good as pointer to tuples(ints)
    2. Minor gains at best

## Semantic data model

THese ideas had little impact on transactional and scalabiliy
