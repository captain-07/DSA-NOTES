---
created: 2026-10-22
revisions:
  - 2026-10-24
  - 2026-10-29
  - 2026-11-06
  - 2026-11-21
---

# Shortest Path in Undirected Graph with Unit Weights

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:**
  - #Amazon #Microsoft #Google #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #graph [[Graph]], #bfs [[Breadth-First Search]], #queue [[Queue]]

## Pattern

Breadth-First Search (Level-Order Traversal)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Since all edge weights are uniform (unit weight = 1), standard Breadth-First Search (BFS) naturally explores nodes in strictly non-decreasing order of distance. The first time a node is visited via BFS is guaranteed to be its shortest path.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Unit weights = standard BFS with a FIFO queue. Initialize distances to $\infty$ (or `-1`), set `dist[src] = 0`, and update neighbors: `dist[nbr] = dist[curr] + 1`.

---

## Approach

### Brute Force
- Run DFS finding all possible paths from source to all destinations and record the minimum length.
- Time Complexity: $O(V!)$ or $O(2^V)$ due to exploring all paths.

### Better
- Dijkstra's Algorithm using a Min-Heap.
- Overkill for unit weights; unnecessary $O(\log V)$ heap overhead per operation.
- Time Complexity: $O((V + E) \log V)$.

### Optimal
- Build adjacency list from edge list.
- Initialize `distance` array of size `V` with `-1` (unreachable) and set `distance[source] = 0`.
- Push `source` into a standard FIFO queue.
- Pop `current_node`, traverse all its unvisited neighbors (`distance[neighbor] == -1`), update `distance[neighbor] = distance[current_node] + 1`, and push them to the queue.

---

## Code (Python)

```python
from collections import deque
from typing import List

class Solution:
    def shortest_path(self, edges: List[List[int]], num_vertices: int, num_edges: int, source: int) -> List[int]:
        # Step 1: Build the undirected adjacency list
        adj_list = [[] for _ in range(num_vertices)]
        for u, v in edges:
            adj_list[u].append(v)
            adj_list[v].append(u)

        # Step 2: Initialize distance array with -1 (unvisited/unreachable)
        distances = [-1] * num_vertices
        distances[source] = 0

        # Step 3: Standard BFS queue
        queue = deque([source])

        # Step 4: Traverse graph level by level
        while queue:
            current_node = queue.popleft()
            current_distance = distances[current_node]

            for neighbor in adj_list[current_node]:
                # If neighbor has not been visited yet
                if distances[neighbor] == -1:
                    distances[neighbor] = current_distance + 1
                    queue.append(neighbor)

        return distances
```

---

## Dry Run (Smart Example)

**Input:** `num_vertices = 4`, `edges = [[0, 1], [1, 2], [0, 2], [2, 3]]`, `source = 0`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `queue = [0]`, `distances = [0, -1, -1, -1]` | Initialize queue with `source = 0`, distance set to `0`. |
| 2 | `curr = 0`, `queue = [1, 2]`, `distances = [0, 1, 1, -1]` | Pop 0. Visit neighbors 1 and 2. Set their distances to `1`, enqueue both. |
| 3 | `curr = 1`, `queue = [2]`, `distances = [0, 1, 1, -1]` | Pop 1. Neighbors are 0 and 2; both already visited (`!= -1`). Do nothing. |
| 4 | `curr = 2`, `queue = [3]`, `distances = [0, 1, 1, 2]` | Pop 2. Neighbor 3 unvisited: set `distances[3] = 2`, enqueue 3. |
| 5 | `curr = 3`, `queue = []`, `distances = [0, 1, 1, 2]` | Pop 3. Neighbor 2 visited. Queue empty, BFS completes. |

---

## Edge Cases

- **Disconnected Components:** Nodes that cannot be reached from `source` remain `-1`.
- **Self-Loops & Multi-Edges:** Unvisited check (`distances[neighbor] == -1`) inherently ignores redundant edges.
- **Single Node Graph:** `num_vertices = 1`, `source = 0` returns `[0]`.
- **Source Node with No Edges:** Returns `0` for source and `-1` for all other vertices.

---

## Mistakes

- User Mistake: No specific note provided.
- Using DFS instead of BFS to find shortest path (DFS does not guarantee shortest path on first visit).
- Using Dijkstra's Algorithm unnecessarily, adding $O(\log V)$ factor when edge weights are uniform.
- Forgetting to mark distance/visited *before* pushing to the queue, causing redundant pushes and TLE/MLE.

---

## Complexity

Time: $O(V + E)$ → Each vertex and edge is processed at most once during queue operations.
Space: $O(V + E)$ → Required for adjacency list, queue, and distance array.

---

## Similar Problems

- [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/) - Medium
- [Word Ladder](https://leetcode.com/problems/word-ladder/) - Hard
- [01 Matrix](https://leetcode.com/problems/01-matrix/) - Medium
- [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #bfs #shortestpath #graphs
- [[Graph]] [[Breadth-First Search]] [[Queue]]
- **Revision Date:** 2026-10-22
- **Problem Link:** [Shortest Path in Undirected Graph with Unit Weights - GeeksforGeeks](https://www.geeksforgeeks.org/problems/shortest-path-in-undirected-graph-having-unit-distance/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-24)
- [ ] Day 7 Revision (2026-10-29)
- [ ] Day 15 Revision (2026-11-06)
- [ ] Day 30 Revision (2026-11-21)
