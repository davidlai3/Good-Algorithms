## Overview
- Used for obtaining the shortest path to all vertices in a weighted graph, given a starting vertex
	- **The graph must be connected and have non-negative weights**
- Most implementations use a priority queue to find the edge with minimum weight
- Time: $O(E + V\log V)$
- Space: $O(V)$
## Approach
1. Initialize distance and seen arrays, as well as a priority queue. `dist[i]` will refer to the total distance required to get to the `ith` vertex from the source vertex
2. Push the source vertex into the priority queue
3. While the priority queue is not empty,
	1. Pop the front element
	2. If that element has been seen, pop the next element 
	3. For every `ith`element that is adjacent to the popped element, calculate the distance it takes to reach it. If it is less than the current value of `dist[i]`, update it.
	4. If the calculated value is less, also push the adjacent vertex onto the priority queue
4. After completing these steps,  `dist[i]` will contain the lengths of the paths to reach vertex `i` in minimal time
## Implementation
- NOTE: C++ priority queues are max-heaps by default. To change it to a min-heap, refer to the initialization below.
- NOTE: At the start of each while loop call, we are guaranteed to be have the minimum distance to reach the node at the front of the queue
```cpp
bool seen[N];
ll int dist[N];

// adjacency list pairs as (weight, vertex)
void dijkstra(const vector<vector<ii>> &adj) {
	fill_n(dist, n+1, INF);
	dist[1] = 0; // starting from vertex 1
	priority_queue<pll, vector<pll>, greater<pll>> pq;
	pq.push(mp(0, 1)); // (distance, vertex)

	while (!pq.empty()) {
		// dequeue closest node
		ii head = pq.top(); pq.pop();
		// these two lines are necessary!
		if (seen[head.snd]) continue;
		else seen[head.snd] = true;
		for (auto v : adj[head.snd]) {
			if (seen[v.snd]) continue;
			if (dist[head.snd] + v.fst < dist[v.snd]) {
				dist[v.snd] = dist[head.snd] + v.fst;
				pq.push(mp(dist[v.snd], v.snd));
			}
		}
	}
}
```
### Problems
- LeetCode #64 - Minimum Path Sum
- CSES - Shortest Routes I