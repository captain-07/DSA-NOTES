---
created: 2026-10-25
revisions:
  - 2026-10-27
  - 2026-11-01
  - 2026-11-09
  - 2026-11-24
---

# Bellman Ford Algorithm

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Google #Amazon #Microsoft #Uber #Directi
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #graph [[Graph]], #shortest-path [[Shortest Path]], #dynamic-programming [[Dynamic Programming]]

## Pattern

Edge Relaxation + Dynamic Programming

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

Relax all $E$ edges $V - 1$ times because a simple shortest path in a graph with $V$ vertices contains at most $V - 1$ edges. Running an extra $V$-th iteration detects negative weight cycles if any distance can still be minimized.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Init `dist[src]=0, others=inf`. Loop `V-1` times over all edges `(u, v, w)`: `dist[v] = min(dist[v], dist[u] + w)`. 1 more pass relaxes = negative cycle.

---

## Approach

### Brute Force
- Explore all possible simple paths from source to all vertices using DFS recursion.
- Time Complexity: $O(V!)$

### Better
- SPFA (Shortest Path Faster Algorithm) / Queue-optimized Bellman-Ford: Only re-relax edges from vertices whose distances were updated in the previous step.
- Time Complexity: $O(V \times E)$ worst case, but $O(E)$ on average.

### Optimal
- Initialize distance array with infinity; set `dist[src] = 0`.
- Iterate $V - 1$ rounds over every edge `(u, v, w)`. If `dist[u] != inf` and `dist[u] + w < dist[v]`, update `dist[v] = dist[u] + w`.
- Run one final ($V$-th) pass across all edges. If any distance further decreases, report a negative cycle.

---

## Code (Python)

```python
class Solution:
    def bellman_ford(self, num_vertices: int, edges: list[list[int]], source: int) -> list[int]:
        # Step 1: Initialize distances from source to all vertices as infinity
        distances = [float('inf')] * num_vertices
        distances[source] = 0

        # Step 2: Relax all edges (V - 1) times
        for _ in range(num_vertices - 1):
            for source_vertex, target_vertex, weight in edges:
                if distances[source_vertex] != float('inf') and distances[source_vertex] + weight < distances[target_vertex]:
                    distances[target_vertex] = distances[source_vertex] + weight

        # Step 3: Check for negative weight cycles with a V-th relaxation pass
        for source_vertex, target_vertex, weight in edges:
            if distances[source_vertex] != float('inf') and distances[source_vertex] + weight < distances[target_vertex]:
                # Negative cycle detected; return empty list or designated flag
                return [-1]

        return distances
```

---

## Dry Run (Smart Example)

Input: `num_vertices = 3`, `edges = [[0, 1, 4], [1, 2, -3], [0, 2, 3]]`, `source = 0`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Initial | `dist = [0, inf, inf]` | Source vertex `0` set to 0, all others `inf`. |
| Pass 1 (Edge `0->1`) | `dist = [0, 4, inf]` | `dist[0] + 4 = 4 < inf`, `dist[1]` updated to 4. |
| Pass 1 (Edge `1->2`) | `dist = [0, 4, 1]` | `dist[1] + (-3) = 1 < inf`, `dist[2]` updated to 1. |
| Pass 1 (Edge `0->2`) | `dist = [0, 4, 1]` | `dist[0] + 3 = 3 > 1`, no update. |
| Pass 2 (All Edges) | `dist = [0, 4, 1]` | All relaxations yield no change; shortest paths stabilized. |
| Pass 3 (Check Cycle) | `dist = [0, 4, 1]` | No distance decreases; confirm no negative cycle exists. |

---

## Edge Cases

- **Negative Weight Cycle:** $V$-th pass successfully detects cycle and prevents infinite loops.
- **Disconnected Vertices:** Unreachable nodes keep `inf`; must guard with `dist[u] != inf` before relaxation.
- **Negative Edges without Cycle:** Correctly finds shortest paths where Dijkstra fails.
- **Single Vertex Graph ($V = 1$):** Loop runs 0 times; immediately returns `[0]`.

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting to verify `dist[u] != inf` before relaxing, which causes overflow or fake updates from unreachable nodes (`inf + negative_wt < inf`).
- Relaxing only once instead of $V - 1$ times.
- Assuming it works for undirected graphs with negative edges without converting each undirected edge into a 2-way negative cycle.

---

## Complexity

Time: $O(V \times E)$ → We perform $V - 1$ iterations, traversing all $E$ edges in each iteration.
Space: $O(V)$ → Distance array of size $V$ to store shortest distances.

---

## Similar Problems

- [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) - Medium
- [Network Delay Time](https://leetcode.com/problems/network-delay-time/) - Medium
- [Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #graph #shortest-path #bellman-ford
- [[Graph]] [[Shortest Path]] [[Dynamic Programming]]
- **Last Revised:** 2026-10-25
- **Problem Link:** [GeeksforGeeks - Bellman-Ford Algorithm](https://www.geeksforgeeks.org/problems/distance-from-the-source-bellman-ford-algorithm/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-27)
- [ ] Day 7 Revision (2026-11-01)
- [ ] Day 15 Revision (2026-11-09)
- [ ] Day 30 Revision (2026-11-24)
