## Overview
- A sparse table is a data structure that allows us to perform range queries over an array in logarithmic time or even constant time
	- Process Time: $O(n\log n)$
	- Query Time: $O(\log n)$ or $O(1)$
	- Space: $O(n\log n)$
- Sparse tables do not handle updates efficiently, running in $O(n\log n)$ time. If you need to handle many updates, consider using a [[Segment Trees]].
## Prerequisites
- A sparse table is only possible when the function $f(l, r)$ is associative. That is, $$f(a, f(b, c)) = f(f(a, b), c)$$
- If the function is "overlap friendly," then the sparse table can answer queries in constant time. Being overlap friendly means that a function will yield the same answer regardless of whether it is combining ranges which overlap or not. More formally, $$f(f(a, b), f(b, c)) = f(a, f(b, c))$$
- Functions like addition are not overlap friendly, while functions like `min()` or `max()` are overlap friendly
## Construction
- The idea behind a sparse table is to precompute the answer for all intervals of size $2^x$ to efficiently answer range queries between $[l, r]$ 
- Let $N$ be the size of the input values array, and $2^P$ be the largest power of $2$ that fits in $N$. Note that we can calculate $P$ as $\text{floor}(log_2(N))$
- From there, we can initialize our table with $P+1$ rows and $N$ columns. The first row will simply be the original input array
- Each cell $(i, j)$ of the table will represent the answer for the range $[j, j + 2^i)$, excluding the first row
- For cells that represent an interval that go beyond the range of the original array, we can simply ignore them
- Because each interval has the length of a power of two, we can always break the interval down into two smaller parts
- Conversely, this means that we can use the first row to build up the sparse table, increasing our spacing as we go. Our recurrence is as follows: $$dp[i][j] = f(dp[i-1][j], dp[i-1][j+2^{i-1}])$$
- For queries that don't have an interval with a size of a power of two, we can break it down into multiple pieces
	- If our function is overlap friendly, then we simply choose one interval that contains the start and another that contains the end
	- Otherwise, we need an interval for each power of two in the range's binary representation
## Additional
- When using a global array to construct your sparse table, the dimensions of your table will always be $sp[\log_2\text{MAXN}+1][\text{MAXN}]$
## Implementation
In these implementations, each cell of the sparse table represents a zero indexed, inclusive range of the original array. The queries also follow this condition.

Overlap friendly (min example):
```cpp
int sp[18][N];

void construct(int n) {
	int k = floor(log2(n));
	for (int i = 0; i < n; i++) cin >> sp[0][i];
	for (int i = 1; i <= k; i++) {
		for (int j = 0; j + (1 << i) <= n; j++) {
			sp[i][j] = sp[i-1][j] ^ sp[i-1][j + (1 << (i-1))];
		}
	}
}

int query(int l, int r) {
	int k = floor(log2(r - l + 1));
	cout << min(sp[k][l], sp[k][r - (1 << k) + 1]) << endl;
}

```

Non-Overlap friendly (xor sum example)
```cpp
// sparse table
// N = 2 * 1e5
int sp[18][N];

void construct(int n) {
	int k = floor(log2(n));
	for (int i = 0; i < n; i++) cin >> sp[0][i];
	for (int i = 1; i <= k; i++) {
		for (int j = 0; j + (1 << i) <= n; j++) {
			sp[i][j] = sp[i-1][j] ^ sp[i-1][j + (1 << (i-1))];
		}
	}
}
// queries are zero-indexed and inclusive on both ends
int query(int l, int r) { 
	int sum = 0;
	for (int j = k; j >= 0; j--) {
		if ((1 << j) <= r - l + 1) {
			sum ^= sp[j][l];
			l += 1 << j;
		}
	}
	cout << sum << endl;
}

```

For more info on sparse tables, visit https://cp-algorithms.com/data_structures/sparse-table.html
## Practice Problems:
- CSES: Static Range Minimum Queries
- CSES: Range Xor Queries