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

Greedy + Priority Queue (Min-Heap) / BFS with Weighted Edges

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

Always greedily expand the currently reachable node with the smallest cumulative distance using a Min-Heap. Because all edge weights are non-negative, the first time a node is popped from the heap, its minimal distance is guaranteed and finalized.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Min-Heap stores `(dist, u)`. If `dist > dist_array[u]`, skip (lazy deletion); otherwise, relax neighbors and push `(new_dist, v)`.

---

## Approach

### Brute Force
- Explore all possible simple paths from source to target using DFS/Backtracking.
- Time Complexity: $O(V!)$ or $O(V \cdot 2^V)$.

### Better
- Unoptimized Dijkstra using an array to find the minimum distance vertex in each iteration.
- Finds min in $O(V)$ each time; overall Time Complexity: $O(V^2 + E) = O(V^2)$.

### Optimal
- Use an adjacency list and a Min-Heap (priority queue) to retrieve the next closest vertex in $O(\log V)$.
- Relax edges and insert updated distances into the heap; skip outdated stale pairs.

---

## Code (Python)

```python
import heapq

class Solution:
    def dijkstra(self, num_nodes: int, edges: list[list[int]], source: int) -> list[int]:
        # Step 1: Build the adjacency list: node -> list of (neighbor, weight)
        adjacency_list = [[] for _ in range(num_nodes)]
        for start_node, end_node, weight in edges:
            adjacency_list[start_node].append((end_node, weight))
            # If undirected: adjacency_list[end_node].append((start_node, weight))

        # Step 2: Initialize min-distances array with infinity
        min_distances = [float('inf')] * num_nodes
        min_distances[source] = 0

        # Step 3: Priority queue stores tuples of (current_distance, node)
        priority_queue = [(0, source)]

        while priority_queue:
            current_distance, current_node = heapq.heappop(priority_queue)

            # Skip if we already found a shorter path to current_node
            if current_distance > min_distances[current_node]:
                continue

            # Step 4: Relax all outgoing edges
            for neighbor, edge_weight in adjacency_list[current_node]:
                new_distance = current_distance + edge_weight

                # Found a strictly shorter path to neighbor
                if new_distance < min_distances[neighbor]:
                    min_distances[neighbor] = new_distance
                    heapq.heappush(priority_queue, (new_distance, neighbor))

        return min_distances
```

---

## Dry Run (Smart Example)

Input: `num_nodes = 3`, `source = 0`, `edges = [[0, 1, 4], [0, 2, 1], [2, 1, 2]]`
Initial: `min_distances = [0, inf, inf]`, `pq = [(0, 0)]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `pop (0, 0)` | Valid pop. Inspect neighbors: relax `1` to `4`, relax `2` to `1`. `pq = [(1, 2), (4, 1)]`, `dist = [0, 4, 1]`. |
| 2 | `pop (1, 2)` | Valid pop. Inspect neighbor `1`: path `1 + 2 = 3 < 4`. Relax `1` to `3`. `pq = [(3, 1), (4, 1)]`, `dist = [0, 3, 1]`. |
| 3 | `pop (3, 1)` | Valid pop. No outgoing edges. `dist` remains `[0, 3, 1]`. |
| 4 | `pop (4, 1)`

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-27)
- [ ] Day 7 Revision (2026-11-01)
- [ ] Day 15 Revision (2026-11-09)
- [ ] Day 30 Revision (2026-11-24)
