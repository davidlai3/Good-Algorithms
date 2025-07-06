## Overview
If we want to merge $k$ sorted lists of length $n$, the best way to do so is with a heap. To take advantage of the fact that the lists are already sorted, we can stipulate that the heap has a maximum size of $k$ at all times, rather than $nk$.
- Time: $O(nk*\log k)$
## Implementation
```cpp
void solution() {
	int k, n; cin >> k >> n;
	vector<vector<int>> a(k, vector<int>(n));
	for (int i = 0; i < k; i++) {
		for (int j = 0; j < n; j++) {
			cin >> a[i][j];
		}
	}
	// Pair = {value, src list}
	priority_queue<ii, vector<ii>, greater<ii>> pq; // min heap
	for (int i = 0; i < k; i++) { // Initializer
		pq.push({a[i][0], i});
	}
	// Starting positions of each list ptr
	vector<int> positions(n, 1)
	vector<int> ans;
	while (!pq.empty()) {
		int val = pq.top().first; int src = pq.top().second;
		ans.push_back(val);
		if (positions[src] < n) {
			pq.push(a[src][positions[src]]);
			positions[src]++;
		}
		pq.pop();
	}
	for (int i = 0; i < n*k; i++) {
		cout << ans[i] << " ";
	}
	cout << endl;
}
```