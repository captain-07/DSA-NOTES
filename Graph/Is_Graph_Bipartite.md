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
- **Target Companies:**
  - #Facebook #Amazon #Google #Microsoft #Bloomberg
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #graph [[Graph]], #bfs [[BFS]], #dfs [[DFS]], #graphcoloring [[Graph Coloring]]

## Pattern

Graph Coloring (2-Coloring) / Bipartite Check (BFS/DFS)

---
## Difficulty

Medium
#medium

---
## ⚡ Key Idea (Core Insight)

A graph is bipartite if and only if it is 2-colorable (contains no odd-length cycles). Assign colors (e.g., 0 and 1) to vertices and ensure every adjacent vertex receives the opposite color; a conflict implies an odd cycle.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Color with 2 alternating colors via BFS/DFS; if any neighbor already has the same color as the current node, return `False`.

---
## Approach

### Brute Force
- Try all $2^V$ vertex colorings and check for conflicts across edges.
- Complexity: $O(2^V \cdot (V + E))$

### Better
- N/A (Standard traversal solves this optimally directly).

### Optimal
- Maintain a `color` array initialized to `-1` (unvisited).
- Iterate through all nodes $0$ to $V-1$ to handle disconnected components.
- For each unvisited node, assign an initial color and traverse using DFS or BFS, assigning `1 - current_color` to all unvisited neighbors.
- If a neighbor already has the same color, return `False`.

---
## Code (Python)

```python
class Solution:
    def isBipartite(self, graph: list[list[int]]) -> bool:
        num_nodes = len(graph)
        # -1 means unvisited, 0 and 1 are the two colors

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-16)
- [ ] Day 7 Revision (2026-10-21)
- [ ] Day 15 Revision (2026-10-29)
- [ ] Day 30 Revision (2026-11-13)
