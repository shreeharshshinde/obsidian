**The "Ripple Effect"**

- **Intuition:** Imagine dropping a stone in a pond. The ripples expand outward in perfect circles. BFS visits nodes in layers: first neighbors (Distance 1), then neighbors of neighbors (Distance 2), etc.
- **Data Structure:** `std::queue` (FIFO - First In, First Out).
- **Key Property:** In an **unweighted** graph, the first time BFS reaches a node, it is via the **shortest path**.

#### The "God-Tier" BFS Template

Use this template for: **Shortest Path**, **Level-order printing**, **Rotting Oranges**.
```cpp
void bfs(int startNode, int n, vector<vector<int>>& adj) {
	queue<int> q;
	vector<bool> visited(n, false); // Crucial to prevent cycles
	
	q.push(startNode);
	visited[startNode] = true;
	
	int level = 0;
	
	while(!q.empty()) {
		int size = q.size();
		
		for(int i=0; i<levelSize; i++) {
			int u = q.front(); q.pop();
			
			// --- Process Node 'u' here --- 
			// if (u == target) return level;
			
			for(int v : adj[u]) {
				if(!visited) {
					visited[v] = true;
					q.push(v);
					// dist[v] = dist[u] + 1; // If tracking specific distances
				}
			}
		}
		
		level++; // Increment distance
	}
}
```

### Grid BFS (The "Rotting Oranges" Pattern)

**Use when:** Shortest path in a grid, Multi-source spreading (fire spreading, virus). **Logic:** "Add starting cell(s) to queue. Process layer by layer using `level` variable."

```cpp
int bfs(vector<vector<int>>& grid, int i, int j, vector<vector<bool>>& visited) {
	int rows = grid.size();
	int cols = grid[0].size();
	
	queue<pair<int,int>> q;
	q.push({i,j});
	visited[i][j] = true;
	
	int level = 0;
	vector<vector<int>> dirs = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}};
	
	while(!q.empty()) {
		int size = q.size();
		
		while(size--) {
			auto node = q.front(); q.pop();
			
			int r = node.first;
			int c = node.second;
			
			if(r == rows - 1 && c == cols - 1) return level;
			for(auto& d : dirs) {
				int nr = r + d[0];
				int nc = c + d[1];
				
				
			}
		}
	}
}
```