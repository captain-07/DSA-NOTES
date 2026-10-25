---
created: 2026-10-25
revisions:
  - 2026-10-27
  - 2026-11-01
  - 2026-11-09
  - 2026-11-24
---

# Dijkstra's Algorithm

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Google #Amazon #Microsoft #Meta #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #graph [[Graph]], #shortestpath [[Shortest Path]], #heap [[Heap]], #greedy [[Greedy]]

## Pattern

Greedy + Min-Heap (Priority Queue) / BFS with Weighted Edges

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Greedily process the unvisited node with the smallest known distance using a Min-Heap. Because all edge weights are non-negative, the first time a node is popped from the heap, its shortest path from the source is finalized.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Min-Heap stores `(distance, node)`. Pop minimum, skip if `distance > dist[node]`, relax neighbors: if `dist[u] + weight < dist[v]`, update and push.

---

## Approach

### Brute Force
- Search all possible simple paths from source to all nodes using exhaustive DFS/backtracking.
- Time Complexity: $O(V!)$

### Better
- Unoptimized Dijkstra using an array to track minimum distances instead of a Min-Heap.
- Scan array linearly in $O(V)$ each step to pick the next min-distance node.
- Time Complexity: $O(V^2 + E) = O(V^2)$

### Optimal
- Use an adjacency list and a Min-Heap (Priority Queue).
- Maintain a `dist` array initialized to $\infty$, with `dist[source] = 0`.
- Push `(0, source)` into heap.
- Pop `(current_dist, u)`. If `current_dist > dist[u]`, continue (stale entry).
- For each neighbor `(v, weight)` of `u`: if `dist[u] + weight < dist[v]`, update `dist[v]` and push `(dist[v], v)`.

---

## Code (Python)

```python
import heapq
from typing import List, Tuple

class Solution:
    def dijkstra(self, num_nodes: int, edges: List[List[int]], source: int) -> List[int]:
        # Step 1: Build the adjacency list: node -> list of (neighbor, weight)
        adj_list = [[] for _ in range(num_nodes)]
        for u, v, weight in edges:
            adj_list[u].append((v, weight))
            adj_list[v].append((u, weight))  # Undirected; omit for directed graphs

        # Step 2: Initialize distances with infinity
        distances = [float('inf')] * num_nodes
        distances[source] = 0

        # Step 3: Min-heap stores tuples of (distance_from_source, node)
        min_heap = [(0, source)]

        # Step 4: Process the priority queue
        while min_heap:
            current_dist, current_node = heapq.heappop(min_heap)

            # Skip outdated entries that were superseded by shorter paths
            if current_dist > distances[current_node]:
                continue

            # Step 5: Relax adjacent edges
            for neighbor, edge_weight in adj_list[current_node]:
                new_dist = current_dist + edge_weight
                if new_dist < distances[neighbor]:
                    distances[neighbor] = new_dist
                    heapq.heappush(min_heap, (new_dist, neighbor))

        return distances
```

---

## Dry Run (Smart Example)

Input: `num_nodes = 3`, `edges = [[0, 1, 4], [0, 2, 1], [2, 1, 2]]`, `source = 0`
Initial: `distances = [0, inf, inf]`, `heap = [(0, 0)]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `pop: (0, 0)`, `heap: []` | Examine neighbors: Node 1 via weight 4 (`dist[1] = 4`), Node 2 via weight 1 (`dist[2] = 1`). Push `(4, 1)` and `(1, 2)`. |
| 2 | `pop: (1, 2)`, `heap: [(4, 1)]` | Examine neighbor: Node 1 via weight 2 (`1 + 2 = 3 < 4`). Update `dist[1] = 3`. Push `(3, 1)`. |
| 3 | `pop: (3, 1)`, `heap: [(4, 1)]` | Shortest path to Node 1 finalized at 3. No unrelaxed outgoing edges. |
| 4 | `pop: (4, 1)`, `heap: []` | `current_dist (4) > distances[1] (3)`. Stale entry skipped. Loop terminates. |

---

## Edge Cases

- **Disconnected Components:** Unreachable nodes keep `float('inf')`.
- **Negative Edge Weights:** Fails; Dijkstra assumes greedy optimality (use Bellman-Ford instead).
- **Self-loops & Multiple Edges:** Min-heap automatically handles and chooses the minimum weight edge.
- **Single Node Graph:** Source is destination; distance is 0.

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting to skip stale entries (`if current_dist > distances[u]: continue`), causing unnecessary edge relaxations and TLE.
- Attempting to use Dijkstra on graphs containing negative edge weights or negative cycles.
- Storing `(node, distance)` instead of `(distance, node)` in Python's `heapq`, which breaks min-distance sorting.

---

## Complexity

Time: $O((V + E) \log V)$ → Each vertex is popped once and each edge relaxed at most once into the min-heap.
Space: $O(V + E)$ → Adjacency list takes $O(V + E)$, heap and distance array store at most $O(V + E)$ elements.

---

## Similar Problems

- [Network Delay Time](https://leetcode.com/problems/network-delay-time/) - Medium
- [Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/) - Medium
- [Path With Minimum Effort](https://leetcode.com/problems/path-with-minimum-effort/) - Medium
- [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #dijkstra #shortestpath [[Shortest Path]] [[Heap]] [[Graph]]
- **Last Revised:** 2026-10-25
- **Problem Link:** [Network Delay Time (Standard Dijkstra LeetCode Model)](https://leetcode.com/problems/network-delay-time/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-27)
- [ ] Day 7 Revision (2026-11-01)
- [ ] Day 15 Revision (2026-11-09)
- [ ] Day 30 Revision (2026-11-24)
