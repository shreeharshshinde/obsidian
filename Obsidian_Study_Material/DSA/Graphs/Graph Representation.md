#### A. Adjacency Matrix

A 2D grid `grid[i][j] = 1` if there is an edge between `i` and `j`.

- **Pros:** $O(1)$ to check if `i` connects to `j`.
- **Cons:** Consumes $O(V^2)$ space.
- **Use when:** $V$ is small ($V < 1000$) or graph is "Dense" (lots of edges).

#### B. Adjacency List (The Standard)

An array of lists. `adj[i]` contains a list of all nodes connected to `i`.

- **Pros:** Space efficient $O(V + E)$. Iterating neighbors is fast.
- **Cons:** $O(Degree)$ to check specific edge connection.
- **Use when:** 95% of interview problems.

```cpp
// Input: edges = [[0,1], [1,2], [0,2]], n = 3
vector<vector<int>> buildGraph(int n, vector<vector<int>>& edges) {
	vector<vector<int>> adj(n);
	
	for(const auto& edge : edges) {
		int u = edge[0], v = edge[1];
		adj[u].push_back(v);
		adj[v].push_back(u);
	}
	return adj;
}
```

## `visited` — The Backbone of Graph Traversal

### What is `visited`?
`visited` is a mechanism to **remember which nodes (or cells) have already been processed** during traversal.

> In graphs, cycles are common.  
> Without `visited`, BFS/DFS can loop forever.

>Mark a node as visited **when you PUSH it** (queue/stack/recursion), not when you POP.

```cpp
vector<bool> visited(n, false); %% For Simple Graphs %%
```

```cpp
vector<vector<bool>> visited(n, vector<bool>(m, false)) %% For Grid Problems %%
```

