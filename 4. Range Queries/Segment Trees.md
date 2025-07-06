# Overview
- Segment trees are data structures that allow us to answer range queries in $O(\log n)$ time. In addition, if we wanted to update the original array, we can also do that in $O(\log n)$ time, while maintaining the correctness of the tree
- Process Time: $O(n)$
- Query Time: $O(\log n)$
- Update Time: $O(\log n)$
- Space: $O(n)$

## Implementation
Note that in this implementation, the bounds on `tl` and `tr` are $0$-based and inclusive. That is the entire array interval is represented by $[0, n-1]$. Any queries or updates made to the segment tree should follow this configuration
```cpp
const int N = 1e5 + 5;
    
int seg[4*N];

// tl: left bound of current tree node
// tr: right bound of current tree node
// idx: index of node in segment tree
void build(const vector<int> &a, int idx, int tl, int tr) {
	if (tl == tr) seg[idx] = a[tl];
	else {
		int tm = (tl+tr) >> 1;
		build(a, idx*2, tl, tm);
		build(a, idx*2+1, tm+1, tr);
		seg[idx] = seg[idx*2] + seg[idx*2+1]; // sum query
	}
}

// Note that two recursive calls are not always necessary, in which case the first check (l > r) gives us an early exit
int query(int idx, int tl, int tr, int l, int r) {
	if (l > r) return 0;
	if (l == tl && r == tr) return seg[idx];
	int tm = (tl+tr) >> 1;
	return query(idx*2, tl, tm, l, min(r, tm)) + 
		query(idx*2+1, tm+1, tr, max(l, tm+1), r);
}

void update(int idx, int tl, int tr, int pos, int new_val) {
	if (tl == tr) { // implied that they are == pos
		seg[idx] = new_val;
		return;
	}
	int tm = (tl+tr) >> 1;
	if (pos <= tm) update(idx*2, tl, tm, pos, new_val);
	else update(idx*2+1, tm+1, tr, pos, new_val);

	seg[idx] = seg[idx*2] + seg[idx*2+1];
}
    
void sol() {
	int n, q; cin >> n >> q;
	vector<int> a(n);
	for (int i = 0; i < n; i++) cin >> a[i];

	// must start at idx 1 because of idx*2
	build(a, 1, 0, n-1);

	for (int i = 0; i < q; i++) {
		int l, r; cin >> l >> r;
		cout << query(1, 0, n-1, l-1, r-1) << endl;
	}
}
```
## Practice Problems
- CSES: Dynamic Range Sum Queries
- CSES: Dynamic Range Min Queries