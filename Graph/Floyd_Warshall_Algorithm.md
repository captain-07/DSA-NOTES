---
created: 2026-10-28
revisions:
  - 2026-10-30
  - 2026-11-04
  - 2026-11-12
  - 2026-11-27
---

# Floyd Warshall Algorithm

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Google #Amazon #Microsoft #Uber #Directi
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #graph [[Graph]], #dynamicprogramming [[Dynamic Programming]], #shortestpath [[Shortest Path]]

## Pattern

All-Pairs Shortest Path (APSP) + Dynamic Programming

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Use dynamic programming by considering each vertex $k$ as an intermediate transition state. The shortest path between $i$ and $j$ using vertices from $\{0 \dots k\}$ is $\min(\text{dist}[i][j], \text{dist}[i][k] + \text{dist}[k][j])$.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Three nested loops with intermediate vertex $k$ in the **outermost loop**: `dist[i][j] = min(dist[i][j], dist[i][k] + dist[k][j])`. Negative cycle detected if `dist[i][i] < 0`.

---

## Approach

### Brute Force
- Run DFS/BFS from every single node to find all simple paths to all other nodes.
- Time Complexity: $O(V \cdot V!)$

### Better
- Run Dijkstra's algorithm from every vertex (fails with negative edge weights).
- Time Complexity: $O(V \cdot (V + E \log V))$ or Bellman-Ford from every vertex $O(V^2 E)$.

### Optimal
- Initialize a 2D distance matrix with direct edge weights and `0` on the diagonal.
- Iterate $k$ from $0$ to $V-1$ (outer loop).
- Iterate all pairs $(i, j)$ and update `dist[i][j]` via intermediate node $k$.
- Check if any `dist[i][i] < 0` to identify negative weight cycles.

---

## Code (Python)

```python
class Solution:
    def floyd_warshall(self, num_vertices: int, edges: list[list[int]]) -> list[list[float]]:
        # Initialize distance matrix with infinity
        inf = float('inf')
        distance = [[inf] * num_vertices for _ in range(num_vertices)]

        # Distance to self is always 0
        for vertex in range(num_vertices):
            distance[vertex][vertex] = 0

        # Fill direct edge weights (u, v, weight)
        for source, destination, weight in edges:
            distance[source][destination] = min(distance[source][destination], weight)

        # k must be the outermost loop (intermediate node)
        for intermediate in range(num_vertices):
            for source in range(num_vertices):
                for destination in range(num_vertices):
                    # Prevent overflow or unnecessary checks if intermediate is unreachable
                    if distance[source][intermediate] != inf and distance[intermediate][destination] != inf:
                        new_distance = distance[source][intermediate] + distance[intermediate][destination]
                        if new_distance < distance[source][destination]:
                            distance[source][destination] = new_distance

        # Check for negative weight cycles
        for vertex in range(num_vertices):
            if distance[vertex][vertex] < 0:
                return [] # Indicates presence of a negative cycle

        return distance
```

---

## Dry Run (Smart Example)

Input: 3 vertices (`0, 1, 2`), Edges: `(0→1: 4)`, `(0→2: 11)`, `(1→2: -2)`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| Initial | `dist` matrix | `dist[0][1]=4`, `dist[0][2]=11`, `dist[1][2]=-2`, diagonal `0`, others `inf` |
| `k=0` | `intermediate=0` | No paths improved using `0` as intermediate. |
| `k=1` | `intermediate=1, i=0, j=2` | `dist[0][2] = min(11, dist[0][1] + dist[1][2]) = min(11, 4 + (-2)) = 2` |
| `k=2` | `intermediate=2` | No further reductions possible. |
| Final | Negative cycle check | All `dist[i][i] == 0`; valid matrix returned with `dist[0][2] = 2`. |

---

## Edge Cases

- **Self-loops with negative weight:** Results in `dist[i][i] < 0` immediately, signaling an invalid graph.
- **Negative weight cycle reachable:** Any entry on diagonal `dist[i][i]` becomes negative.
- **Disconnected components:** Paths between components remain `inf`; guard against updating `inf + weight`.
- **Parallel edges:** Multiple edges between same $u \to v$; initialize with `min(edge_weight)`.

---

## Mistakes

- Placing intermediate node loop $k$ in the inner loop instead of the outermost loop.
- Missing the infinity check before addition, causing unintended updates or overflow.
- User mistake: No specific note provided.

---

## Complexity

Time: $O(V^3)$ → Three nested loops each running $V$ times.
Space: $O(V^2)$ → 2D matrix required to store all-pairs shortest path distances.

---

## Similar Problems

- [Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/) - Medium
- [Network Delay Time](https://leetcode.com/problems/network-delay-time/) - Medium
- [Course Schedule IV](https://leetcode.com/problems/course-schedule-iv/) - Medium
- [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #graph #floydwarshall #dynamicprogramming
- [[Graph]] [[Dynamic Programming]] [[Shortest Path]]
- **Last Revised:** 2026-10-28
- **Problem Link:** [GeeksforGeeks - Floyd Warshall](https://www.geeksforgeeks.org/problems/implementing-floyd-warshall2042/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-30)
- [ ] Day 7 Revision (2026-11-04)
- [ ] Day 15 Revision (2026-11-12)
- [ ] Day 30 Revision (2026-11-27)
