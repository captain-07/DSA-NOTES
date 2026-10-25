---
created: 2026-10-22
revisions:
  - 2026-10-24
  - 2026-10-29
  - 2026-11-06
  - 2026-11-21
---

# Shortest Path in Directed Acyclic Graph

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Microsoft #Google #Flipkart
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #topologicalsort [[Topological Sort]], #shortestpath [[Shortest Path]], #dag [[Directed Acyclic Graph]], #dynamicprogramming [[Dynamic Programming]]

## Pattern

Topological Sort + Dynamic Programming (Relaxation)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

In a DAG, processing vertices in **topological order** guarantees that whenever a node $u$ is processed, the shortest distances to all predecessor nodes that lead into $u$ are already finalized. We can relax its outgoing edges in a single pass without needing a min-heap.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Toposort first to linearize dependencies $\to$ Relax outgoing edges in topological order $\to$ Done in $O(V + E)$ time.

---
## Approach

### Brute Force
- Find all possible paths from source to all nodes using DFS/backtracking and take the minimum path weight.
- Time Complexity: $O(V!)$ or $O(2^V)$ in worst case.

### Better
- Run Dijkstra's Algorithm using a min-heap priority queue.
- Handles non-negative weights in $O((V + E) \log V)$, but does not work reliably with negative edge weights and is slower than optimal.

### Optimal
- Step 1: Compute Topological Sort ordering using Kahn's algorithm (indegree BFS) or DFS.
- Step 2: Initialize distance array `dist` with $\infty$, setting `dist[source] = 0`.
- Step 3: Iterate through nodes in topological order; if `dist[u] != infinity`, relax each directed edge $(u, v, weight)$: `dist[v] = min(dist[v], dist[u] + weight)`.
- Handles negative edge weights as long as the graph is acyclic.

---
## Code (Python)

```python
from collections import deque
from typing import List

class Solution:
    def _get_topological_order(self, num_nodes: int, adj_list: List[List[tuple]]) -> List[int]:
        indegree = [0] * num_nodes
        for u in range(num_nodes):
            for v, _ in adj_list[u]:
                indegree[v] += 1

        queue = deque()
        for node in range(num_nodes):
            if indegree[node] == 0:
                queue.append(node)

        topo_order = []
        while queue:
            curr_node = queue.popleft()
            topo_order.append(curr_node)
            for neighbor, _ in adj_list[curr_node]:
                indegree[neighbor] -= 1
                if indegree[neighbor] == 0:
                    queue.append(neighbor)

        return topo_order

    def shortestPath(self, num_nodes: int, num_edges: int, edges: List[List[int]]) -> List[int]:
        adj_list = [[] for _ in range(num_nodes)]
        for u, v, weight in edges:
            adj_list[u].append((v, weight))

        topo_order = self._get_topological_order(num_nodes, adj_list)

        # Source vertex is assumed to be 0
        distances = [float('inf')] * num_nodes
        distances[0] = 0

        # Relax edges in topological order
        for node in topo_order:
            if distances[node] != float('inf'):
                for neighbor, weight in adj_list[node]:
                    if distances[node] + weight < distances[neighbor]:
                        distances[neighbor] = distances[node] + weight

        # Replace unreachable nodes with -1
        for i in range(num_nodes):
            if distances[i] == float('inf'):
                distances[i] = -1

        return distances
```

---
## Dry Run (Smart Example)

Input: `num_nodes = 4`, `edges = [[0, 1, 2], [0, 2, 4], [1, 2, -3], [2, 3, 1]]`, `source = 0`
Topological Order: `[0, 1, 2, 3]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `node = 0`, `dist = [0, inf, inf, inf]` | Relax edges $(0, 1, 2) \to dist[1] = 2$, $(0, 2, 4) \to dist[2] = 4$. |
| 2 | `node = 1`, `dist = [0, 2, 4, inf]` | Relax edge $(1, 2, -3) \to dist[2] = \min(4, 2 + (-3)) = -1$. Distance updated! |
| 3 | `node = 2`, `dist = [0, 2, -1, inf]` | Relax edge $(2, 3, 1) \to dist[3] = \min(\infty, -1 + 1) = 0$. |
| 4 | `node = 3`, `dist = [0, 2, -1, 0]` | No outgoing edges to relax. Final distances computed. |

---
## Edge Cases

- **Disconnected Graph / Unreachable Nodes:** Nodes before source in topological order remain at $\infty$ (convert to `-1`).
- **Negative Edge Weights:** Correctly handled because the absence of cycles prevents negative cycle loops.
- **Single Node Graph:** Source is the only node; distance array is `[0]`.
- **Multiple Paths to Same Node:** Topological order ensures all incoming alternatives are relaxed before moving forward.

---
## Mistakes

- **Why we use toposort:** In general graphs, we need Dijkstra (priority queue) or Bellman-Ford because cycles force multiple re-relaxations. In a DAG, topological sort orders vertices such that for every directed edge $u \to v$, $u$ comes before $v$. This guarantees that by the time we reach $v$, all possible routes leading into $v$ have already been relaxed, making a single linear pass sufficient and optimal.
- Forgetting to skip nodes with `dist[u] == infinity` (unreachable from source), which could otherwise cause invalid relaxations with negative edge weights.
- Attempting to use Dijkstra when negative edge weights are present (Dijkstra fails with negative edges, but Toposort + DP works).

---
## Complexity

Time: $O(V + E)$ → Building graph, Kahn's algorithm, and relaxing each edge exactly once.
Space: $O(V + E)$ → Adjacency list, indegree array, queue, and distance table.

---
## Similar Problems

- [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) - Medium
- [Longest Increasing Path in a Matrix](https://leetcode.com/problems/longest-increasing-path-in-a-matrix/) - Hard
- [Network Delay Time](https://leetcode.com/problems/network-delay-time/) - Medium
- [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) - Medium

---
## Tags and Properties

- #dsa #important #revisit
- #graph #dag #toposort #shortestpath
- [[Topological Sort]] [[Graph Traversal]] [[Relaxation]]
- **Date:** 2026-10-22
- **Problem Link:** [GeeksforGeeks - Shortest Path in Directed Acyclic Graph](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-24)
- [ ] Day 7 Revision (2026-10-29)
- [ ] Day 15 Revision (2026-11-06)
- [ ] Day 30 Revision (2026-11-21)
