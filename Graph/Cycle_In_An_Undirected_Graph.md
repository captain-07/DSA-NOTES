---
created: 2026-10-08
revisions:
  - 2026-10-10
  - 2026-10-15
  - 2026-10-23
  - 2026-11-07
---

# Cycle in an Undirected Graph

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Microsoft #Google #Facebook #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #graph [[Graph]], #bfs [[Breadth-First Search]], #dfs [[Depth-First Search]], #disjointset [[Disjoint Set Union]]

## Pattern

BFS Traversal with Parent Tracking / Union-Find

---
## Difficulty

Medium
Tag: #medium

---

## ⚡ Key Idea (Core Insight)

In an undirected graph, a cycle exists if during traversal (BFS/DFS) we reach an already visited node that is **not** the immediate parent of the current node. Alternatively, using Union-Find, if two vertices of an edge belong to the same connected component, a cycle exists.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Visited node && node != parent ➔ Cycle Detected!
- Union-Find: `find(u) == find(v)` ➔ Cycle Detected!

---

## Approach

### Brute Force
- Run DFS from every node checking all paths for simple cycles.
- Time: O(V * (V + E)) | Space: O(V)

### Optimal 1: BFS Traversal
- Store pairs of `(current_node, parent_node)` in a queue.
- Mark nodes visited. If a neighbor is visited and `neighbor != parent`, cycle exists.
- Time: O(V + E) | Space: O(V)

### Optimal 2: Union-Find (Disjoint Set Union)
- Initialize parent array where each node is its own parent.
- For each edge `(u, v)`, find absolute parents of `u` and `v`. If equal, cycle found; else `union(u, v)`.
- Time: O(E * α(V)) | Space: O(V)

---

## Code (Python)

```python
from collections import deque

class Solution:
    def isCycleBFS(self, num_vertices: int, adj_list: list[list[int]]) -> bool:
        visited = [False] * num_vertices

        # Check for disconnected graph components
        for start_node in range(num_vertices):
            if not visited[start_node]:
                # Queue stores tuples of (current_node, parent_node)
                queue = deque([(start_node, -1)])
                visited[start_node] = True

                while queue:
                    curr_node, parent_node = queue.popleft()

                    for neighbor in adj_list[curr_node]:
                        if not visited[neighbor]:
                            visited[neighbor] = True
                            queue.append((neighbor, curr_node))
                        # If neighbor is visited and not parent, cycle exists
                        elif neighbor != parent_node:
                            return True

        return False

    def isCycleUnionFind(self, num_vertices: int, edges: list[list[int]]) -> bool:
        parent = list(range(num_vertices))

        def find(node: int) -> int:
            if parent[node] != node:
                parent[node] = find(parent[node])  # Path compression
            return parent[node]

        for u, v in edges:
            root_u = find(u)
            root_v = find(v)

            # Both vertices share the same root -> Cycle detected
            if root_u == root_v:
                return True

            parent[root_u] = root_v  # Union step

        return False
```

---

## Dry Run (Smart Example)

Input: `num_vertices = 4`, `edges = [[0, 1], [1, 2], [2, 3], [3, 1]]` (Cycle at 1-2-3-1)

| Step | Node/Edge | Variables (`queue` / `parent`) | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Start at `0` | `queue=[(0, -1)]`, `visited=[T, F, F, F]` | Push node 0 with no parent |
| 2 | Pop `(0, -1)` | `queue=[(1, 0)]`, `visited=[T, T, F, F]` | Visit neighbor 1, set parent to 0 |
| 3 | Pop `(1, 0)` | `queue=[(2, 1), (3, 1)]`, `visited=[T, T, T, T]` | Visit neighbors 2 and 3, set parent to 1 |
| 4 | Pop `(2, 1)` | Neighbor `3` is visited, `parent=1` | Neighbor 3 is visited and `3 != 1` ➔ **Cycle Detected** |

---

## Edge Cases

- **Disconnected Graph:** Handled by iterating outer loop over all nodes `0` to `V-1`.
- **Self Loops:** Edge `(u, u)` is an immediate cycle (Union-Find handles `find(u) == find(u)`).
- **Parallel Edges:** Two edges between same pair of nodes form a cycle.
- **Linear Graph (Tree):** No cycle present; returns `False`.

---

## Mistakes

- Forgetting to pass and track the `parent` node during BFS/DFS traversal.
- Mistaking visited status alone as a cycle (visited parent node is valid).
- Not handling disconnected components.
- User Mistake: No specific note provided.

---

## Complexity

Time: O(V + E) → BFS visits every vertex once and checks all adjacent edges.
Space: O(V) → Visited array of size V and BFS queue size up to V.

---

## Similar Problems

- [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium
- [Redundant Connection](https://leetcode.com/problems/redundant-connection/) - Medium
- [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) - Medium
- [Graph Valid Tree](https://leetcode.com/problems/graph-valid-tree/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #graph #bfs #dfs #unionfind
- [[Graph]], [[Breadth-First Search]], [[Disjoint Set Union]]
- **Revision Date:** 2026-10-08
- **Problem Link:** [GeeksforGeeks - Detect Cycle in an Undirected Graph](https://www.geeksforgeeks.org/problems/detect-cycle-in-an-undirected-graph/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-10)
- [ ] Day 7 Revision (2026-10-15)
- [ ] Day 15 Revision (2026-10-23)
- [ ] Day 30 Revision (2026-11-07)
