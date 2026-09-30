---
created: 2026-09-30
revisions:
  - 2026-10-02
  - 2026-10-07
  - 2026-10-15
  - 2026-10-30
---

# Connected Components In An Undirected Graph

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #dfs [[Depth First Search]], #bfs [[Breadth First Search]], #disjointset [[Disjoint Set Union]]

## Pattern

Graph Traversal (DFS/BFS) / Disjoint Set Union (DSU)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- Treat the graph as an adjacency list and keep track of visited nodes.
- Iterating through all nodes, whenever an unvisited node is found, trigger a traversal (DFS/BFS) or DSU union operation to discover and collect all nodes reachable in that component.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Loop `0` to `V-1`: If not visited, trigger DFS/BFS to traverse all connected nodes and increment component count.

---

## Approach

### Brute Force
- Check all pairs of vertices `(u, v)` using individual pathfinding queries (e.g., executing full search per pair) to group connected components.
- Time: O(V³), Space: O(V + E)

### Optimal 1: Depth First Search (DFS) / BFS
- Build adjacency list from edges.
- Maintain a `visited` array/set of size `V`.
- Iterate through each node `0` to `V - 1`. If node is unvisited, launch DFS/BFS to visit all reachable nodes and store them in the current component.

### Optimal 2: Disjoint Set Union (DSU / Union-Find)
- Initialize Parent array `parent[i] = i`.
- For each edge `(u, v)`, find root representative of `u` and `v`. If different, perform `union(u, v)`.
- Group nodes by their root parent to extract all components.

---

## Code (Python)

```python
class Solution:
    def _dfs(self, node: int, adj: list[list[int]], visited: list[bool], component: list[int]) -> None:
        visited[node] = True
        component.append(node)

        # Traverse all unvisited neighbors of the current node
        for neighbor in adj[node]:
            if not visited[neighbor]:
                self._dfs(neighbor, adj, visited, component)

    def connectedcomponents(self, v: int, edges: list[list[int]]) -> list[list[int]]:
        # Step 1: Build the adjacency list for undirected graph
        adj = [[] for _ in range(v)]
        for u, w in edges:
            adj[u].append(w)
            adj[w].append(u)

        visited = [False] * v
        components = []

        # Step 2: Iterate through all nodes to find unvisited components
        for node in range(v):
            if not visited[node]:
                current_component = []
                self._dfs(node, adj, visited, current_component)
                components.append(current_component)

        return components
```

---

## Dry Run (Smart Example)

Input: `v = 5`, `edges = [[0, 1], [1, 2], [3, 4]]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `node = 0`, `visited = [F,F,F,F,F]` | Node 0 is unvisited. Start DFS. Visits 0, then neighbor 1, then neighbor 2. |
| 2 | `visited = [T,T,T,F,F]`, `components` | Component 1 completed: `[0, 1, 2]`. |
| 3 | `node = 1, 2` | Nodes 1 and 2 are already visited. Skip. |
| 4 | `node = 3`, `visited = [T,T,T,F,F]` | Node 3 is unvisited. Start DFS. Visits 3, then neighbor 4. |
| 5 | `visited = [T,T,T,T,T]`, `components` | Component 2 completed: `[3, 4]`. Output: `[[0, 1, 2], [3, 4]]`. |

---

## Edge Cases

- **Disconnected Graph (No edges):** Every node forms its own component of size 1.
- **Single Component (Fully Connected Graph):** Returns 1 component containing all `V` vertices.
- **Graph with Isolated Nodes:** Isolated vertices must be included as individual components.
- **Empty Graph (`v = 0`):** Returns empty list `[]`.

---

## Mistakes

- Forgetting to make the adjacency list bidirectional for undirected graphs.
- Failing to handle isolated nodes that have no edges.
- User mistake: No specific note provided.

---

## Complexity

Time: O(V + E) → Every vertex and edge is visited once during traversal.
Space: O(V + E) → Storage for adjacency list, visited array, and DFS recursion stack.

---

## Similar Problems

- [Number of Islands](https://leetcode.com/problems/number-of-islands/) - Medium
- [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) - Medium
- [Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/) - Medium
- [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) - Medium

---

## Tags and Properties

  - #dsa #important #revisit
  - #graph #dfs #bfs #disjointset
  - [[Graph]], [[Depth First Search]], [[Disjoint Set Union]]
  - **Revision Date:** 2026-09-30
  - **Problem Link:** [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-02)
- [ ] Day 7 Revision (2026-10-07)
- [ ] Day 15 Revision (2026-10-15)
- [ ] Day 30 Revision (2026-10-30)
