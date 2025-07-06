## Overview
- Multisets are a type of sorted associative container similar to the set, with the exception that multiple elements can have the same value. The underlying data structure is typically a self-balancing binary search tree. **Multisets, similar to sets, are non decreasing by default**.
- When you remove an element from a multiset with `erase` , it removes all occurrences of that element. This can be avoided with `ms.erase(find(value))`, or in C++ 17, `ms.extract(value)`.
- Operations:
	- `insert(x)`: $O(\log n)$
	- `clear()`: $O(n)$
	- `erase()`: O(\log n)
	- `upper_bound(x)`: $O(\log n)$
	- `lower_bound(x)`: $O(\log n)$