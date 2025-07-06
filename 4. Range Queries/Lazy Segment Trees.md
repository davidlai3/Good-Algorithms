## Overview
Segment trees are useful because they allow us to perform both range queries and updates on an array, but what if we wanted to update multiple elements in a range at a time? We could just call the `update` function on every element on our desired range, but there is a better way to do this: **lazy propagation**.
Lazy propagation allows us to postpone some updates, and only do the updates when required. This is done through the addition of a `lazy[]` array, which stores update information for the tree.
## Approach
Suppose that a call to `query` is made for the tree. Then, we have 