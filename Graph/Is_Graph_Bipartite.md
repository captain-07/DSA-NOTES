---
created: 2026-10-14
revisions:
  - 2026-10-16
  - 2026-10-21
  - 2026-10-29
  - 2026-11-13
---

# Is Graph Bipartite?

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Facebook #Google #Microsoft #Bloomberg

- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #graph [[Graph]], #bfs [[Breadth-First Search]], #dfs [[Depth-First Search]], #graphcoloring [[Graph Coloring]]

## Pattern

Graph Coloring (2-Coloring) via BFS / DFS

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

A graph is bipartite if and only if it contains no odd-length cycles. We can verify this by attempting a 2-coloring: assign each node a color (e.g., `1` and `-1`), and ensure all its neighbors are assigned the opposite color.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Color each unvisited node `1`, then use BFS/DFS to color neighbors with `-color`. If a neighbor has the same color, return `False`. Handle disconnected components with an outer loop.

---

## Approach

### Brute Force
- Generate all $2^V$ vertex partitions into two sets and check if any partition has zero internal edges.
- Time Complexity: $O(2^V \cdot (V + E))$

### Better
- Not applicable; standard traversal (BFS/DFS) directly achieves optimal linear time.

### Optimal
- Maintain a `colors` array initialized to `0` (unvisited).
- Iterate through all nodes $0$ to $V-1$ to handle disconnected components.
- If a node is uncolored, assign it color `1` and start DFS/BFS.
- For each neighbor:
  - If unvisited: assign `opposite_color` and recurse/push to queue.
  - If already visited: check if its color equals the current node's color. If yes, return `False`.
- Return `True` if no conflicts are found across all components.

---

## Code (Python)

```python
class Solution:
    def _dfs_check(self, current_node: int, current_color: int, graph: list[list[int]], colors: list[int]) -> bool:
        # Assign color to the current node
        colors[current_node] = current_color

        # Determine the opposite color for all adjacent neighbors
        neighbor_color = -current_color

        for neighbor in graph[current_node]:
            if colors[neighbor] == 0:
                # Recursively color the unvisited neighbor
                if not self._dfs_check(neighbor, neighbor_color, graph, colors):
                    return False
            elif colors[neighbor] == current_color:
                # Conflict: neighbor has the same color
                return False

        return True

    def isBipartite(self, graph: list[list[int]]) -> bool:
        num_nodes = len(graph)
        # 0: unvisited, 1: red, -1: blue
        colors = [0] * num_nodes

        # Loop through all nodes to handle disconnected components
        for node in range(num_nodes):
            if colors[node] == 0:
                # Start DFS by coloring the unvisited component root with 1
                if not self._dfs_check(node, 1, graph, colors):
                    return False

        return True
```

---

## Dry Run (Smart Example)

Input: `graph = [[1, 2, 3], [0, 2], [0, 1, 3], [0, 2]]` (Odd cycle between nodes 0, 1, 2)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `node=0`, `colors=[1, 0, 0, 0]` | Node 0 colored `1`. Inspect neighbors: `[1, 2, 3]`. |
| 2 | `node=1`, `colors=[1, -1, 0, 0]` | Neighbor 1 is unvisited. Colored `-1`. Inspect neighbors: `[0, 2]`. |
| 3 | `node=2`, `colors=[1, -1, 1, 0]` | From node 1, neighbor 2 is unvisited. Colored `1`. Inspect neighbors: `[0, 1, 3]`. |
| 4 | `node=2`, neighbor `0`, `colors[0]=1` | Neighbor 0 has color `1`, which matches node 2's color `1`. Conflict detected $\rightarrow$ return `False`. |

---

## Edge Cases

- **Disconnected Graph:** Handled by outer loop over all nodes `0` to $V-1$.
- **Isolated Vertices (no edges):** Valid bipartite; trivially colored `1`.
- **Self-loops / Multiple Components:** Handled by neighbor color check.
- **Even Cycles (e.g., $C_4$):** Always bipartite; alternates correctly with no conflicts.

---

## Mistakes

- **User Mistake:** Do not toggle the color at the beginning of DFS; assign the intended color passed into the call or toggle strictly when transitioning to neighbors (`-color`).
- Forgetting that the graph may have disconnected components and only running traversal from node `0`.
- Toggling the color in-place globally or flipping it prematurely before exploring all neighbors.
- Overwriting an already colored node's color instead of validating equality.

---

## Complexity

Time: O(V + E) → Every vertex and edge is visited at most once during the traversal.
Space: O(V) → Recursion call stack and `colors` array of size $V$.

---

## Similar Problems

- [Possible Bipartition](https://leetcode.com/problems/possible-bipartition/) - Medium
- [Clone Graph](https://leetcode.com/problems/clone-graph/) - Medium
- [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium
- [Word Ladder](https://leetcode.com/problems/word-ladder/) - Hard

---

## Tags and Properties

- #dsa #important #revisit #graph #dfs #bfs #coloring
- Concepts: [[Graph]], [[Depth-First Search]], [[Breadth-First Search]], [[Bipartite Graph]]
- **Last Revised:** 2026-10-14
- **Problem Link:** [LeetCode - Is Graph Bipartite?](https://leetcode.com/problems/is-graph-bipartite/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-16)
- [ ] Day 7 Revision (2026-10-21)
- [ ] Day 15 Revision (2026-10-29)
- [ ] Day 30 Revision (2026-11-13)
