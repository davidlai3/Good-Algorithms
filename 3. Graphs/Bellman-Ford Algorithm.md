## Overview
- Used for finding the single-source shortest path in a graph, given that the graph can have negative edge weights. It can also be used to detect negative edge weight cycles in a graph. It is important to note that even with a negative edge weight cycle, there can still be a shortest path as the cycle may not lead to the target vertex.
- Time: $O(V*E)$
- Space: $O(V)$
## Approach
1. Initialize a distance array of size $n$ (number of vertices), where every entry is initially infinity.
2. Set the distance of the source vertex to 0.
3. Go through the set of all edges. If any edge $(e, v)$ has a source $e$ whose distance is not infinity, then relax that edge (update the distance to $v$ if smaller).
4. Repeat step 3 $n-1$ times. If you want to detect for negative edge weight cycles, then repeat step 3 $n$ times. If we can relax an edge on the $n$th iteration, then there must be a negative edge weight cycle.
## Implementation
```cpp
void sol() {
	int n, m; cin >> n >> m;
	vector<iii> edges(m);
	for (int i = 0; i < m; i++) {
		int x, y, w; cin >> x >> y >> w;
		x--; y--; // optional
		edges[i].push_back({x, y, w});
	}

	vector<int> dist(n, INT_MAX);
	dist[0] = 0;

	bool neg_cycle = false;
	for (int i = 0; i < n; i++) {
		bool any_relax = false;
		for (int j = 0; j < m; j++) {
			int x = get<0>(edges[j]);
			int y = get<1>(edges[j]);
			int w = get<2>(edges[j]);

			if (dist[x] == INT_MAX) continue;
			if (dist[x] + w < dist[y]) {
				any_relax = true;
				if (i == n-1) neg_cycle = true;
				dist[y] = dist[x] + w;
			}
		}
		if (!any_relax) break; // early exit optimization
	}
	if (neg_cycle) cout << -1 << endl;
	else {
		for (int i = 0; i < n; i++) {
			cout << dist[i] << " ";
		}
		cout << endl;
	}
}
```
