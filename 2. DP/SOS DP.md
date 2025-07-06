## Overview
- Sum over subsets (SOS) DP is a trick that allows us to efficiently compute the sum over all subsets of an array

Suppose we have some array $a[0], a[1], \ldots, a[2^{k}-1]$. Each index of the array represents the included elements in a set and the value of the array represents that subset's associated value. Define $$A[x] = \sum\limits_{i \subseteq x} a[i] $$
That is, $A(x)$ is the sum over all subsets $i$ such that $i$ is a subset of $x$ (in bits). We want to calculate $A[0], A[1], \ldots, A[2^{k} - 1]$
```cpp
for (int x = 0; x < (1 << k) - 1; i++) {
	for (int y = k; y >= 0; y = (y - 1) & x) { // skip over bad masks
		A[x] += a[y];
	}
}
```
This gives us a time complexity $O(3^k)$.