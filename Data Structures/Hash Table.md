
## 1. Collision resolution by chaining

In chaining, if a hash function produces the same index for multiple elements, these elements are stored in the same index by using a doubly-linked list.

If `j` is the slot for multiple elements, it contains a pointer to the head of the list of elements. If no element is present, `j` contains `NIL`.

![Collision Resolution using chaining](Attachments/Hash-3_1.webp)


## 2. Open Addressing

Unlike chaining, open addressing doesn't store multiple elements into the same slot. Here, each slot is either filled with a single key or left `NIL`.

Different techniques used in open addressing are:

### i. Linear Probing

In linear probing, collision is resolved by checking the next slot.

$$h(k, i) = (h′(k) + i) \text{ mod } m$$

where

-   `i = {0, 1, ….}`
-   `h'(k)` is a new hash function

If a collision occurs at `h(k, 0)`, then `h(k, 1)` is checked. In this way, the value of `i` is incremented linearly.

The problem with linear probing is that a cluster of adjacent slots is filled. When inserting a new element, the entire cluster must be traversed. This adds to the time required to perform operations on the hash table.

### ii. Quadratic Probing

It works similar to linear probing but the spacing between the slots is increased (greater than one) by using the following relation.

$$h(k, i) = (h′(k) + c_1 \cdot i + c_2 \cdot i^2) \text{ mod } m$$

where,

-   `c1` and `c2` are positive auxiliary constants,
-   `i = {0, 1, ….}`

### iii. Double hashing

If a collision occurs after applying a hash function `h(k)`, then another hash function is calculated for finding the next slot.

$$h(k, i) = (h_1(k) + i \cdot h_2(k)) \text{ mod } m$$
