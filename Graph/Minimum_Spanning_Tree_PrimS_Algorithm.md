---
created: 2026-10-30
revisions:
  - 2026-11-01
  - 2026-11-06
  - 2026-11-14
  - 2026-11-29
---

# Minimum Spanning Tree Prim'S Algorithm

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Microsoft #Google #Cisco
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [x] High
- **Concepts:** #graph [[Graph]], #greedy [[Greedy]], #heaps [[Min-Heap]]

## Pattern

Greedy + Min-Heap (Priority Queue)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Start from an arbitrary node, grow the MST by greedily picking the minimum-weight edge connecting an visited node to an unvisited node using a Min-Heap. Repeat until all $V$ nodes are included.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Min-Heap stores `(weight, node)`. Pop smallest, mark visited, add weight to MST sum, and push unvisited neighbors.

---

## Approach

### Brute Force
- Check all possible subsets of $V - 1$ edges to see if they form an acyclic connected tree, then find the minimal weight sum.
- Time Complexity: $O(\binom{E}{V-1} \cdot V)$

### Better
- Adjacency matrix representation with an array to find the minimum cut edge at each step.
- Time Complexity: $O(V^2)$

### Optimal
- Use an adjacency list and a Min-Heap (priority queue) to retrieve the minimum-weight crossing edge in $O(\log E)$ time.
- Track visited vertices to prevent cycles.

---

## Code (Python)

```python
import heapq

class Solution:
    def spanningTree(self, num_vertices: int, adj_list: list[list[list[int]]]) -> int:
        # Min-Heap stores tuples: (edge_weight, current_node)
        min_heap = [(0, 0)]
        visited = [False] * num_vertices
        total_mst_weight = 0
        edges_included = 0

        while min_heap and edges_included < num_vertices:
            weight, current_node = heapq.heappop(min_heap)

            # Skip if node is already part of the MST
            if visited[current_node]:
                continue

            # Include current node in MST
            visited[current_node] = True
            total_mst_weight += weight
            edges_included += 1

            # Traverse all adjacent neighbors
            for neighbor, edge_weight in adj_list[current_node]:
                if not visited[neighbor]:
                    heapq.heappush(min_heap, (edge_weight, neighbor))

        return total_mst_weight
```

---

## Dry Run (Smart Example)

Input: `num_vertices = 3`, Edges: `0-1 (w=5)`, `1-2 (w=3)`, `0-2 (w=1)`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `heap=[(0, 0)]`, `visited=[F, F, F]`, `sum=0` | Pop `(0, 0)`. Mark `0` visited. Push `(5, 1)`, `(1, 2)`. |
| 2 | `heap=[(1, 2), (5, 1)]`, `visited=[T, F, F]`, `sum=0` | Pop `(1, 2)`. Mark `2` visited. `sum = 1`. Push `(3, 1)`. |
| 3 | `heap=[(3, 1), (5, 1)]`, `visited=[T, F, T]`, `sum=1` | Pop `(3, 1)`. Mark `1` visited. `sum = 4`. All nodes visited. |
| 4 | `edges_included = 3` | Terminate. Return `total_mst_weight = 4`. |

---

## Edge Cases

- **Disconnected Graph:** Cannot form an MST covering all nodes (check `edges_included == num_vertices`).
- **Parallel Edges with Different Weights:** Min-heap automatically prioritizes the minimum weight edge.
- **Single Node Graph ($V=1$):** Total weight is `0` as 0 edges are needed.
- **Self Loops:** Ignored as visited checks and cycle avoidance prevent self-inclusion.

---

## Mistakes

- User Mistake: No specific note provided.
- Pushing to heap without checking if neighbor is already visited, bloating heap size.
- Forgetting to skip visited nodes upon `heappop` (heap can hold stale multiple entries for the same node).
- Confusing Prim's (vertex-centric, best for dense graphs) with Kruskal's (edge-centric with DSU, best for sparse graphs).

---

## Complexity

Time: $O(E \log E)$ or $O(E \log V)$ → Each edge is pushed to the min-heap at most once.
Space: $O(V + E)$ → Adjacency list, visited array, and min-heap storage.

---

## Similar Problems

- [Connecting Cities With Minimum Cost](https://leetcode.com/problems/connecting-cities-with-minimum-cost/) - Medium
- [Min Cost to Connect All Points](https://leetcode.com/problems/min-cost-to-connect-all-points/) - Medium
- [Find Critical and Pseudo-Critical Edges in MST](https://leetcode.com/problems/find-critical-and-pseudo-critical-edges-in-minimum-spanning-tree/) - Hard

---

## Tags and Properties

- #dsa #important #revisit
- #minimum-spanning-tree #prims-algorithm #graph-algorithms
- [[Minimum Spanning Tree]] [[Prim's Algorithm]] [[Graph]]
- **Revision Date:** 2026-10-30
- **Problem Link:** [GeeksforGeeks - Minimum Spanning Tree](https://www.geeksforgeeks.org/problems/minimum-spanning-tree/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-11-01)
- [ ] Day 7 Revision (2026-11-06)
- [ ] Day 15 Revision (2026-11-14)
- [ ] Day 30 Revision (2026-11-29)
