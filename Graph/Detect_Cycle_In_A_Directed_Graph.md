---
created: 2026-10-14
revisions:
  - 2026-10-16
  - 2026-10-21
  - 2026-10-29
  - 2026-11-13
---

# Detect Cycle in a Directed Graph

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Flipkart

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #graph [[Graph]], #dfs [[DFS]], #bfs [[BFS]], #topologicalsort [[Topological Sort]]

## Pattern

DFS with Path Tracking / Kahn's Algorithm (BFS Topological Sort)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

- **DFS:** A cycle exists if and only if a back-edge is found pointing to a node currently in the active recursion call stack (`in_path`).
- **BFS (Kahn's):** A directed acyclic graph (DAG) always admits a full topological sort. If total processed nodes with in-degree zero is less than total vertices `V`, a cycle exists.

---

## ⚡ Quick Recall (VERY IMPORTANT)

DFS: standard `visited` vs active `path_visited` state (or 3-color marking).
BFS: Kahn's algorithm; if `processed_count != total_vertices`, cycle detected!

---

## Approach

### Brute Force
- Enumerate all possible paths starting from every node up to length `V`; check if any path loops back to an earlier node.
- Time Complexity: $O(V!)$ or exponential.

### Better
- Run separate DFS/BFS traversals from every node to see if the origin node is reachable from itself.
- Improvement Idea: Track reachability per vertex. Time Complexity: $O(V \cdot (V + E))$.

### Optimal
- **Method 1 (DFS - 3 States / Path Visited):**
  1. Maintain `visited` array (global seen) and `in_path` array (current recursion branch).
  2. For current node, mark both true. Recurse on neighbors.
  3. If neighbor is already `in_path`, cycle found!
  4. Unmark `in_path[node]` on backtracking.
- **Method 2 (BFS - Kahn's Algorithm):**
  1. Calculate in-degrees for all nodes; enqueue all nodes with `in_degree == 0`.
  2. Pop from queue, increment `processed_count`, reduce in-degrees of neighbors.
  3. Push neighbor to queue if its in-degree reaches `0`.
  4. Return `processed_count != num_nodes`.

---

## Code (Python)

```python
from collections import deque
from typing import List

class Solution:
    # ------------------ OPTIMAL 1: DFS APPROACH ------------------
    def is_cycle_dfs(self, num_nodes: int, adj_list: List[List[int]]) -> bool:
        visited = [False] * num_nodes
        in_path = [False] * num_nodes

        # Check every connected component
        for node in range(num_nodes):
            if not visited[node]:
                if self.check_cycle_dfs(node, adj_list, visited, in_path):
                    return True
        return False

    def check_cycle_dfs(self, curr_node: int, adj_list: List[List[int]], visited: List[bool], in_path: List[bool]) -> bool:
        visited[curr_node] = True
        in_path[curr_node] = True

        for neighbor in adj_list[curr_node]:
            if not visited[neighbor]:
                if self.check_cycle_dfs(neighbor, adj_list, visited, in_path):
                    return True
            # Back-edge detected: neighbor is in current recursion stack
            elif in_path[neighbor]:
                return True

        # Backtrack: remove from current path
        in_path[curr_node] = False
        return False

    # ------------------ OPTIMAL 2: BFS (KAHN'S) APPROACH ------------------
    def is_cycle_bfs(self, num_nodes: int, adj_list: List[List[int]]) -> bool:
        in_degree = [0] * num_nodes

        # Step 1: Compute in-degree for all vertices
        for node in range(num_nodes):
            for neighbor in adj_list[node]:
                in_degree[neighbor] += 1

        # Step 2: Push all nodes with 0 in-degree to queue
        queue = deque()
        for node in range(num_nodes):
            if in_degree[node] == 0:
                queue.append(node)

        processed_count = 0

        # Step 3: Standard BFS topological ordering
        while queue:
            curr_node = queue.popleft()
            processed_count += 1

            for neighbor in adj_list[curr_node]:
                in_degree[neighbor] -= 1
                if in_degree[neighbor] == 0:
                    queue.append(neighbor)

        # If not all nodes are processed, cycle exists
        return processed_count != num_nodes
```

---

## Dry Run (Smart Example)

Input: `num_nodes = 4`, Directed Edges: `0 -> 1, 1 -> 2, 2 -> 3, 3 -> 1` (Cycle: 1 -> 2 -> 3 -> 1)

| Step | Current Node / State | Action / Variables | Explanation |
|---|---|---|---|
| 1 | Node `0` (DFS) | `visited={0}`, `in_path={0}` | Traverses `0 -> 1`. |
| 2 | Node `1` (DFS) | `visited={0,1}`, `in_path={0,1}` | Moves deeper to `2`, then `3`. |
| 3 | Node `3` (DFS) | `visited={0,1,2,3}`, `in_path={0,1,2,3}` | Examines neighbor `1`. `visited[1]` is True AND `in_path[1]` is True. |
| 4 | Cycle Confirmed | Return `True` | Back-edge to an ancestor node in the active path detected. |

---

## Edge Cases

- **Self-loop (`u -> u`):** Immediately detected as `in_path[u]` or `in_degree` never hits 0.
- **Disconnected components:** Must iterate over all nodes `0` to `V-1` as start points.
- **Pure DAG without cycles:** Traversal finishes without returning `True`; BFS processes all `V` nodes.
- **Graph with cross-edges (Diamond `0->1, 0->2, 1->3, 2->3`):** Node 3 is revisited via separate path; `visited[3] == True` but `in_path[3] == False` prevents false positive cycle.

---

## Mistakes

- Using only a single `visited` array in DFS (fails on cross-edges in DAGs; you must track `in_path`).
- Forgetting to backtrack `in_path[curr_node] = False` when exiting the DFS frame.
- Failing to know both DFS and BFS implementations (interviewers frequently ask to pivot from DFS recursion to Kahn's BFS).
- In BFS, mistaking `processed_count == num_nodes` for presence of cycle instead of absence of cycle.

---

## Complexity

Time: $O(V + E)$ → Each vertex is visited once and each edge is traversed once.
Space: $O(V)$ → Auxiliary arrays (`visited`, `in_path` or `in_degree`) and queue/call-stack size of at most $V$.

---

## Similar Problems

- [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium
- [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) - Medium
- [Find Eventual Safe States](https://leetcode.com/problems/find-eventual-safe-states/) - Medium
- [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) - Hard

---

## Tags and Properties

- #dsa #important #revisit #graph #dfs #bfs #topologicalsort
- [[Graph]] [[Depth First Search]] [[Breadth First Search]] [[Topological Sort]]
- **Revision Date:** 2026-10-14
- **Problem Link:** [Course Schedule - LeetCode](https://leetcode.com/problems/course-schedule/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-16)
- [ ] Day 7 Revision (2026-10-21)
- [ ] Day 15 Revision (2026-10-29)
- [ ] Day 30 Revision (2026-11-13)
