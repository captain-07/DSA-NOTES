---
created: 2026-09-30
revisions:
  - 2026-10-02
  - 2026-10-07
  - 2026-10-15
  - 2026-10-30
---

# Dfs In Graph

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Google #Microsoft #Facebook #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #dfs [[Depth-First Search]], #graph [[Graph Traversal]], #recursion [[Recursion]]

## Pattern

Depth-First Search (DFS) / Graph Traversal

---
## Difficulty

Easy / Medium #easy #medium

---

## ⚡ Key Idea (Core Insight)

- Explore as deep as possible along each branch before backtracking.
- Use a `visited` array/set to prevent infinite loops in cyclic or undirected graphs.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Recursive call for every unvisited neighbor; backtrack automatically via call stack.

---

## Approach

### Brute Force
- Traverse paths without tracking visited nodes, leading to infinite loops on cycles.
- Time: O(∞) on cyclic graphs.

### Optimal
- Maintain a `visited` set/list.
- Start from a node, mark it visited, add to traversal result, and recursively visit all its unvisited adjacent nodes.
- For disconnected graphs, iterate through all vertices and launch DFS if not yet visited.

---

## Code (Python)

```python
class Solution:
    def dfsOfGraph(self, num_nodes: int, adj: list[list[int]]) -> list[int]:
        visited = [False] * num_nodes
        traversal_result = []

        # Start DFS from vertex 0 (or iterate all vertices for disconnected graph)
        self._dfs_helper(0, adj, visited, traversal_result)
        return traversal_result

    def _dfs_helper(self, curr_node: int, adj: list[list[int]], visited: list[bool], result: list[int]) -> None:
        # Mark current node as visited and append to result
        visited[curr_node] = True
        result.append(curr_node)

        # Traverse all unvisited neighbors
        for neighbor in adj[curr_node]:
            if not visited[neighbor]:
                self._dfs_helper(neighbor, adj, visited, result)
```

---

## Dry Run (Smart Example)

Input: `num_nodes = 4`, `adj = [[1, 2], [0, 3], [0], [1]]` (0-indexed graph)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `curr_node = 0`, `visited = [T, F, F, F]` | Visit 0, add to `result = [0]`. Neighbors of 0 are `[1, 2]`. Call DFS(1). |
| 2 | `curr_node = 1`, `visited = [T, T, F, F]` | Visit 1, add to `result = [0, 1]`. Neighbors of 1 are `[0, 3]`. Neighbor 0 visited, call DFS(3). |
| 3 | `curr_node = 3`, `visited = [T, T, F, T]` | Visit 3, add to `result = [0, 1, 3]`. Neighbor 1 is visited. Return to DFS(1). |
| 4 | `curr_node = 2`, `visited = [T, T, T, T]` | Backtrack to 0, call DFS(2). Visit 2, add to `result = [0, 1, 3, 2]`. Return. |

---

## Edge Cases

- **Disconnected Graph:** Must loop over all vertices to ensure full coverage.
- **Self-loops / Multiple edges:** Visited array handles self-loops cleanly.
- **Single Node Graph:** Traversal returns just `[0]` immediately.
- **Linear/Line Graph:** Recursion depth equals number of nodes; watch stack depth limits.

---

## Mistakes

- User mistake: No specific note provided.
- Forgetting to track visited nodes resulting in recursion overflow/infinite loops.
- Not handling disconnected components when required by problem statement.

---

## Complexity

Time: O(V + E) → Every vertex (V) and edge (E) is visited once.
Space: O(V) → Visited array of size V and recursion stack up to depth O(V).

---

## Similar Problems

- [BFS of Graph](https://geeksforgeeks.org/problems/bfs-traversal-of-graph/1) - Easy
- [Number of Islands](https://leetcode.com/problems/number-of-islands/) - Medium
- [Clone Graph](https://leetcode.com/problems/clone-graph/) - Medium

---

## Tags and Properties

  - #dsa #important #revisit #dfs #graph #recursion
  - Obsidian links: [[Depth-First Search]], [[Graph Traversal]]
  - Revision Date: 2026-09-30
  - **Problem Link:** [DFS of Graph - GeeksforGeeks](https://www.geeksforgeeks.org/problems/depth-first-traversal-for-a-graph/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-02)
- [ ] Day 7 Revision (2026-10-07)
- [ ] Day 15 Revision (2026-10-15)
- [ ] Day 30 Revision (2026-10-30)
