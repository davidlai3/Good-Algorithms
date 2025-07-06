## Overview
- The Floyd-Warshall is an all-pairs shortest path algorithm, unlike single source shortest path algorithms like [[Dijkstra's Algorithm]] or Bellman Ford. It works for both directed and undirected weighted graphs, but not for graphs with negative cycles (negative weights are okay).
- The idea is to treat all vertices in the graph as intermediate vertices, similar to how you would in Dijkstra's Algorithm.
- Time: $O(V^3)$
- Space: $O(V^2)$
## Implementation
```cpp
// Note: This algorithm mutates the original adjacency matrix
#define INFINITY 1e9
vector<vector<int>> floyd_warshall(vector<vector<int>> dist, int n) {
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < n; j++) {
			for (int k = 0; k < n; k++) {
				// checking to avoid overflow
				if (dist[i][j] > (dist[i][k] + dist[k][j]) 
				&& (dist[i][k] != INF) && (dist[k][j] != INF)) {
					dist[i][j] = dist[i][k] + dist[k][j];
				}
			}
		}
	}
}
```
