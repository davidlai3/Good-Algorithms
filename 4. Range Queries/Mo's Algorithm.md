## Overview
- Mo's Algorithm is an extension of [[Sqrt Decomposition]] that can answer range queries in $O((N+Q)\sqrt{N})$ time, where $N$ is the size of the array and $Q$ is the number of queries
- Mo's algorithm is **offline**, meaning that it requires knowing all the queries beforehand to run
- The idea is to answer the queries in a special order based on the indices. We will first answer all queries which have the left index in block 0, then answer all queries which have left index in block 1 and so on
## Steps
- Parse all queries and array values
- Sort all queries primarily by $\left\lfloor \frac{L_i}{\sqrt{N}} \right\rfloor$, and secondarily by $R_i$  
- Initialize left and right pointers to start of array
- Initialize an accumulator or any required structure to keep track of result
- Iterate through sorted queries, shifting left and right pointers as necessary

## Implementation
```cpp
struct Query {
	int l, r, idx;
};

int main() {
	int n;
	cin >> n;
	vector<int> v(n);
	for (int i = 1; i <= n; i++) { cin >> v[i]; }

	int q;
	cin >> q;
	vector<Query> queries;
	for (int i = 0; i < q; i++) {
		int x, y;
		cin >> x >> y;
		queries.push_back({x, y, i});
	}

	int block_size = (int)sqrt(n);
	auto mo_cmp = [&](Query a, Query b) {
		int block_a = a.l / block_size;
		int block_b = b.l / block_size;
		if (block_a == block_b) { return a.r < b.r; }
		return block_a < block_b;
	};
	sort(queries.begin(), queries.end(), mo_cmp);

	int different_values = 0;
	vector<int> values(VALMAX);
	auto remove = [&](int idx) {
		values[v[idx]]--;
		if (values[v[idx]] == 0) { different_values--; }
	};
	auto add = [&](int idx) {
		values[v[idx]]++;
		if (values[v[idx]] == 1) { different_values++; }
	};

	int mo_left = -1;
	int mo_right = -1;
	vector<int> ans(q);
	for (int i = 0; i < q; i++) {
		int left = queries[i].l;
		int right = queries[i].r;

		while (mo_left < left) { remove(mo_left++); }
		while (mo_left > left) { add(--mo_left); }
		while (mo_right < right) { add(++mo_right); }
		while (mo_right > right) { remove(mo_right--); }

		ans[queries[i].idx] = different_values;
	}

	for (int i = 0; i < q; i++) { cout << ans[i] << '\n'; }
}
```