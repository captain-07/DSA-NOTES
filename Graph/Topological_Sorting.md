---
created: 2026-10-14
revisions:
  - 2026-10-16
  - 2026-10-21
  - 2026-10-29
  - 2026-11-13
---

# Topological Sorting

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Google #Microsoft #Meta #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #graph [[Graph]], #bfs [[Breadth-First Search]], #dfs [[Depth-First Search]], #dag [[DAG]]

## Pattern

Kahn's Algorithm (BFS + In-degree) / Post-order DFS + Reverse

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Linear ordering of vertices in a Directed Acyclic Graph (DAG) where for every directed edge `u -> v`, vertex `u` comes before `v`.
- **BFS (Kahn's):** Repeatedly pick vertices with in-degree 0, reduce neighbors' in-degrees.
- **DFS:** Perform post-order traversal; push vertex to a stack/list after visiting all descendants, then reverse.

---

## ⚡ Quick Recall (VERY IMPORTANT)

BFS: Track `in_degree`, push zeroes into queue.
DFS: Standard DFS with `visited` set, append to result on return path, reverse at end.

---

## Approach

### Brute Force
- Try all $V!$ permutations of vertices and check if every edge $u \to v$ has $u$ appearing before $v$.
- Time Complexity: $O(V! \cdot (V + E))$

### Optimal 1: Kahn's Algorithm (BFS)
1. Compute in-degree for every vertex.
2. Initialize queue with all vertices having `in_degree == 0`.
3. Pop from queue, add to topological order, decrement in-degree of all neighbors.
4. If neighbor's in-degree becomes 0, push to queue.
5. If result length $< V$, graph contains a cycle.

### Optimal 2: Post-Order Traversal (DFS)
1. Maintain `visited` array (`0` = unvisited, `1` = visiting, `2` = visited).
2. For each unvisited node, run DFS.
3. If a neighbor is in state `1`, a cycle exists.
4. After exploring all outgoing edges, append current node to `order`.
5. Reverse `order` at the end to get topological sort.

---

## Code (Python)

```python
from collections import deque
from typing import List

class Solution:
    # ----------------- Approach 1: BFS (Kahn's Algorithm) -----------------
    def topo_sort_bfs(self, num_vertices: int, adj_list: List[List[int]]) -> List[int]:
        in_degree = [0] * num_vertices

        # Step 1: Compute in-degree for every node
        for source in range(num_vertices):
            for neighbor in adj_list[source]:
                in_degree[neighbor] += 1

        # Step 2: Queue nodes with 0 incoming edges
        queue = deque()
        for node in range(num_vertices):
            if in_degree[node] == 0:
                queue.append(node)

        topo_order = []

        # Step 3: Process nodes level by level
        while queue:
            curr_node = queue.popleft()
            topo_order.append(curr_node)

            for neighbor in adj_list[curr_node]:
                in_degree[neighbor] -= 1
                if in_degree[neighbor] == 0:
                    queue.append(neighbor)

        # If graph has a cycle, topological sort is impossible
        if len(topo_order) != num_vertices:
            return []

        return topo_order

    # ----------------- Approach 2: DFS (Post-order Traversal) -----------------
    def topo_sort_dfs(self, num_vertices: int, adj_list: List[List[int]]) -> List[int]:
        # 0: unvisited, 1: visiting (in current recursion stack), 2: visited
        state = [0] * num_vertices
        topo_order = []

        for node in range(num_vertices):
            if state[node] == 0:
                if not self._dfs(node, adj_list, state, topo_order):
                    return []  # Cycle detected

        # Reverse post-order to get topological order
        topo_order.reverse()
        return topo_order

    def _dfs(self, curr_node: int, adj_list: List[List[int]], state: List[int], topo_order: List[int]) -> bool:
        state[curr_node] = 1  # Mark as visiting

        for neighbor in adj_list[curr_node]:
            if state[neighbor] == 1:
                return False  # Back-edge found -> cycle
            if state[neighbor] == 0:
                if not self._dfs(neighbor, adj_list, state, topo_order):
                    return False

        state[curr_node] = 2  # Mark as visited
        topo_order.append(curr_node)  # Add after all dependencies explored
        return True
```

---

## Dry Run (Smart Example)

Input: `num_vertices = 4`, Edges: `1 -> 0`, `2 -> 0`, `3 -> 1`, `3 -> 2` (DAG with multiple branches)

| Step | Queue / Stack | In-Degree / State | Action / Explanation |
| :--- | :--- | :--- | :--- |
| **0** | `Q = [3]` | `[2, 1, 1, 0]` | Node `3` has `in_degree == 0`; start BFS. |
| **1** | `Q = [1, 2]` | `[2, 0, 0, 0]` | Pop `3` $\to$ Order: `[3]`. Decrement neighbors `1, 2`. Both hit 0, added to queue. |
| **2** | `Q = [2]` | `[1, 0, 0, 0]` | Pop `1` $\to$ Order: `[3, 1]`. Decrement neighbor `0` (`in_degree = 1`). |
| **3** | `Q = [0]` | `[0, 0, 0, 0]` | Pop `2` $\to$ Order: `[3, 1, 2]`. Decrement neighbor `0` (`in_degree = 0`), enqueue `0`. |
| **4** | `Q = []` | `[0, 0, 0, 0]` | Pop `0` $\to$ Order: `[3, 1, 2, 0]`. Queue empty, length == 4, valid. |

---

## Edge Cases

- **Cycle Present:** Graph is not a DAG; both methods must detect and return empty list.
- **Disconnected Components:** Graph has isolated vertices; outer loop must check all vertices.
- **Already Sorted / Linear Chain:** Handled naturally from head to tail.
- **No Edges (All Isolated):** All nodes enter queue/result in arbitrary order.

---

## Mistakes

- Must know and implement **both DFS and BFS methods** (interviewers often ask for one specific variation).
- Forgetting cycle detection: BFS checks `len(result) == V`; DFS requires a 3-state tracking array.
- In DFS, forgetting to reverse the accumulated list at the end.
- Modifying the adjacency list directly instead of tracking in-degrees in BFS.

---

## Complexity

Time: $O(V + E)$ → Visits each vertex once and traverses every directed edge once.
Space: $O(V + E)$ → Adjacency list, in-degree/state array, and queue/recursion call stack take $O(V)$.

---

## Similar Problems

- [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium
- [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) - Medium
- [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) - Hard
- [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #topologicalsort #dag #graph-traversal
- Concepts: [[Graph]], [[Topological Sort]], [[Kahn's Algorithm]], [[Cycle Detection]]
- **Revision Date:** 2026-10-14
- **Problem Link:** [Course Schedule II (LeetCode)](https://leetcode.com/problems/course-schedule-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-16)
- [ ] Day 7 Revision (2026-10-21)
- [ ] Day 15 Revision (2026-10-29)
- [ ] Day 30 Revision (2026-11-13)
