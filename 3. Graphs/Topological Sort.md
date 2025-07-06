## Overview
- A topological sort of a directed acyclic graph is a linear ordering of its vertices such that for every directed edge $u\to v$ from vertex $u$ to vertex $v$,  $u$  comes before $v$ in the ordering. There are two approaches for implementing: A queue based approach and a DFS-based approach.
- In other words, each node is sorted based on ascending degree
- Time: $O(V + E)$
- Space : $O(V + E)$
## Applications
- Can be used to find shortest/longest path in a weighted DAG
- Determining if a directed graph has a cycle
- Resolving dependencies (such as determining the order to perform activities)
- [[Kosaraju's Algorithm]]
## Steps
1. Pick an unvisited source (degree 0 node).
2. Do a depth-first traversal starting with that node and only explore unvisited nodes.
3. After visiting child nodes (post-order), add the parent node to the front of a list. 
4. Repeat until all nodes are visited.
- The list will contain a topological sort of the nodes.
## Implementation: DFS
```c++
vector<int> top_sort;
vector<vector<int>> graph;
vector<bool> visited;

void dfs(int node) {
	for (int next : graph[node]) {
		if (!visited[next]) {
			visited[next] = true;
			dfs(next);
		}
	}
	top_sort.push_back(node);
}

int main() {
	int n, m;  // The number of nodes and edges respectively
	std::cin >> n >> m;

	graph = vector<vector<int>>(n);
	for (int i = 0; i < m; i++) {
		int a, b;
		std::cin >> a >> b;
		graph[a - 1].push_back(b - 1);
	}

	visited = vector<bool>(n);
	for (int i = 0; i < n; i++) {
		if (!visited[i]) {
			visited[i] = true;
			dfs(i);
		}
	}
	std::reverse(top_sort.begin(), top_sort.end());

	vector<int> ind(n);
	for (int i = 0; i < n; i++) { ind[top_sort[i]] = i; }

	// Check if the topological sort is valid
	bool valid = true;
	for (int i = 0; i < n; i++) {
		for (int j : graph[i]) {
			if (ind[j] <= ind[i]) {
				valid = false;
				goto answer;
			}
		}
	}
answer:;

	if (valid) {
		for (int i = 0; i < n - 1; i++) { cout << top_sort[i] + 1 << ' '; }
		cout << top_sort.back() + 1 << endl;
	} else {
		cout << "IMPOSSIBLE" << endl;
	}
}
```

## Implementation: Queue (Kahn's Algorithm)
```cpp

void sol() {
	int n, m; cin >> n >> m;
	vector<vector<int>> adj(n);
	for (int i = 0; i < m; i++) {
		int u, v; cin >> u >> v;
		adj[u].push_back(v);
	}
	vector<int> ins(n, 0);
	for (int i = 0; i < n; i++) {
		for (int j = 0; j < adj[i].size(); j++) {
			ins[adj[i][j]]++;
		}
	}

	queue<int> topo;
	// push sources
	for (int i = 0; i < n; i++) {
		if (ins[i] == 0) topo.push(i);
	}

	vector<int> topo_sort(n);
	int cnt = 0;
	while (cnt < n) {
		if (!topo.size()) break; // this must mean there's a cycle
		int x = topo.front(); topo.pop();
		topo_sort[cnt++] = x++;
		for (int i = 0; i < adj[x].size()) {
			ins[adj[x][i]]--;
			if (ins[adj[x][i]] == 0) {
				topo.push(adj[x][i]);
			}
		}
	}
}
```