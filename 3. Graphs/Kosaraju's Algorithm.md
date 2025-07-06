## Overview
- Kosaraju's Algorithm is an algorithm used for detecting strongly connected components in a directed graph.
- Time: $O(|V| + |E|)$

## Steps
1. Perform a series of depth first searches over the graph until all nodes have been visited
	1. For each vertex, we keep track of the exit time $t_{out}[v]$. This is the "timestamp" at which the DFS starting from vertex $v$ finishes (basically topo sort)
	2. This counter is NOT reset between consecutive DFS calls
2. We define the exit time $t_{out}[C]$  of a strongly connected component as the maximum of the values $t_{out}[v]$ for all $v \in C$
	- Conversely, $t_{in}[C]$ is defined as the minimum of the values $t_{in}[v]$ for all $v \in C$
3. **Theorem**: Let $C$ and $C'$ be two different strongly connected components. Let there be a directed edge from $C$ to $C'$ in the condensation graph. Then, $t_{out}[C] > t_{out}[C']$
	- Essentially, this means that any edge in the condensation graph goes from a larger value of $t_{out}$ to a smaller value
4. If we sort all the vertices $v \in V$ in decreasing order of $t_{out}[v]$, then the first vertex $u$ will belong to the "root" strongly connected component, which has no incoming edges in the condensation graph. Think of this as a source vertex, and note the similarity to [[Topological Sort]].
5. **Theorem**: Let $G^T$ denote the transpose graph of $G$, obtained by reversing the edge directions $G$. Then $SCC(G) = SCC(G^T)$. Furthermore, the condensation graph of $G^T$ is the transpose of the condensation graph of $G$
	- Find proof on cpalgorithms loool
6. To find the elements in the root strongly connected component, represented by vertex $v$, we can run a DFS on that vertex in the graph $G^T$. This will visit precisely all vertices of this strongly connected component
7. After we detect the first component, we can remove all vertices associated with it and repeat our algorithm

In summary,
1. Run a sequence of depth first searches on $G$, which will yield some list of vertices, sorted on increasing exit time $t_{out}$
2. Build the transpose graph $G^T$, and run a series of depth first searches on the vertices in reverse order. each depth first search will yield one strongly connected component
3. Optionally, build the corresponding condensation graph

## Implementation

```cpp
vector<bool> visited; // keeps track of which vertices are already visited

// runs depth first search starting at vertex v.
// each visited vertex is appended to the output vector when dfs leaves it.
void dfs(int v, vector<vector<int>> const& adj, vector<int> &output) {
    visited[v] = true;
    for (auto u : adj[v])
        if (!visited[u])
            dfs(u, adj, output);
    output.push_back(v);
}

// input: adj -- adjacency list of G
// output: components -- the strongy connected components in G
// output: adj_cond -- adjacency list of G^SCC (by root vertices)
void strongy_connected_components(vector<vector<int>> const& adj,
                                  vector<vector<int>> &components,
                                  vector<vector<int>> &adj_cond) {
    int n = adj.size();
    components.clear(), adj_cond.clear();

    vector<int> order; // will be a sorted list of G's vertices by exit time

    visited.assign(n, false);

    // first series of depth first searches
    for (int i = 0; i < n; i++)
        if (!visited[i])
            dfs(i, adj, order);

    // create adjacency list of G^T
    vector<vector<int>> adj_rev(n);
    for (int v = 0; v < n; v++)
        for (int u : adj[v])
            adj_rev[u].push_back(v);

    visited.assign(n, false);
    reverse(order.begin(), order.end());

    vector<int> roots(n, 0); // gives the root vertex of a vertex's SCC

    // second series of depth first searches
    for (auto v : order)
        if (!visited[v]) {
            std::vector<int> component;
            dfs(v, adj_rev, component);
            sort(component.begin(), component.end());
            components.push_back(component);
            int root = component.front();
            for (auto u : component)
                roots[u] = root;
        }

    // add edges to condensation graph
    adj_cond.assign(n, {});
    for (int v = 0; v < n; v++)
        for (auto u : adj[v])
            if (roots[v] != roots[u])
                adj_cond[roots[v]].push_back(roots[u]);
}
```