---
created: 2026-10-28
revisions:
  - 2026-10-30
  - 2026-11-04
  - 2026-11-12
  - 2026-11-27
---

# Network Delay Time

---

## Metadata & Placement Tags

- **Folder:** Graph
- **Target Companies:** #Amazon #Google #Microsoft #Meta
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:** #graph [[Graph]], #shortestpath [[Shortest Path]], #heap [[Heap]], #dijkstra [[Dijkstra]]

## Pattern

Shortest Path + Dijkstra's Algorithm (Min-Heap)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

The time it takes for all nodes to receive the signal is the maximum of the shortest travel times from source $k$ to every reachable node. Since edge weights are non-negative, Dijkstra's algorithm efficiently computes the single-source shortest path to all nodes.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Build adjacency list $\to$ Run Dijkstra with Min-Heap `(time, node)` $\to$ If visited count $< n$, return $-1$, else return $\max(\text{times})$.

---

## Approach

### Brute Force
- Run Depth-First Search (DFS) exploring all simple paths to find the minimum arrival time per node.
- Time Complexity: $O(V!)$ or exponential due to exploring all paths.

### Better
- Bellman-Ford / SPFA: Relax all $E$ edges up to $V - 1$ rounds.
- Handles negative edges (not needed here) with time complexity $O(V \cdot E)$.

### Optimal (Dijkstra's Algorithm)
1. Build an adjacency list mapping `u -> (v, weight)`.
2. Use a min-heap initialized with `(0, k)` and a `visited` hash map / distance array storing the minimal time to reach each node.
3. Pop the node with the smallest accumulated time. If already visited, skip.
4. Otherwise, mark it visited, update the max signal time, and push all unvisited neighbors `(curr_time + weight, neighbor)` into the heap.
5. If `len(visited) == n`, return the max time recorded; otherwise, return `-1`.

---

## Code (Python)

```python
import heapq
import collections

class Solution:
    def networkDelayTime(self, times: list[list[int]], n: int, k: int) -> int:
        # Build adjacency list: u -> list of (weight, v)
        graph = collections.defaultdict(list)
        for source, target, travel_time in times:
            graph[source].append((travel_time, target))

        # Min-heap stores tuples of (accumulated_time, current_node)
        min_heap = [(0, k)]
        shortest_path = {}

        while min_heap:
            time_to_curr, current_node = heapq.heappop(min_heap)

            # Skip if we already finalized the shortest path for this node
            if current_node in shortest_path:
                continue

            shortest_path[current_node] = time_to_curr

            # Explore all outgoing neighbors
            for travel_time, neighbor in graph[current_node]:
                if neighbor not in shortest_path:
                    heapq.heappush(min_heap, (time_to_curr + travel_time, neighbor))

        # If all nodes received the signal, return the maximum delay
        if len(shortest_path) == n:
            return max(shortest_path.values())
        return -1
```

---

## Dry Run (Smart Example)

**Input:** `times = [[2,1,1],[2,3,1],[3,4,1]]`, `n = 4`, `k = 2`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `heap = [(0, 2)]`, `shortest_path = {}` | Start at source node `2` with time `0`. |
| 2 | Pop `(0, 2)`. `shortest_path = {2: 0}`. `heap = [(1, 1), (1, 3)]` | Visit `2`. Push neighbors `1` (time 1) and `3` (time 1). |
| 3 | Pop `(1, 1)`. `shortest_path = {2: 0, 1: 1}`. `heap = [(1, 3)]` | Visit `1`. Node `1` has no outgoing edges. |
| 4 | Pop `(1, 3)`. `shortest_path = {2: 0, 1: 1, 3: 1}`. `heap = [(2, 4)]` | Visit `3`. Push neighbor `4` with total time $1 + 1 = 2$. |
| 5 | Pop `(2, 4)`. `shortest_path = {2: 0, 1: 1, 3: 1, 4: 2}`. `heap = []` | Visit `4`. Heap is empty. `len(shortest_path) == 4`, result = `max(...) = 2`. |

---

## Edge Cases

- **Disconnected Graph:** Source cannot reach some nodes $\to$ return `-1`.
- **Single Node Graph ($n = 1$):** Source is the only node $\to$ returns `0`.
- **Multiple Edges Between Same Nodes:** Heap automatically processes the smaller weight first and ignores duplicates.
- **Cycles / Feedback Loops:** Handled correctly by skipping nodes already finalized in `shortest_path`.

---

## Mistakes

- User Mistake: No specific note provided.
- Forgetting to skip nodes that have already been finalized (`if current_node in shortest_path: continue`), causing redundant expansions.
- Returning the sum of edge weights along a path instead of the maximum of all shortest path distances.
- Assuming 0-indexed nodes when the problem is 1-indexed ($1$ to $n$).

---

## Complexity

Time: $O(E \log V)$ → Each edge is added to the min-heap at most once; heap operations take $O(\log V)$.
Space: $O(V + E)$ → Adjacency list takes $O(E)$, heap and distance map store up to $O(V)$ entries.

---

## Similar Problems

- [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) - Medium
- [Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/) - Medium
- [Find the City With the Smallest Number of Neighbors at a Threshold Distance](https://leetcode.com/problems/find-the-city-with-the-smallest-number-of-neighbors-at-a-threshold-distance/) - Medium
- [Swim in Rising Water](https://leetcode.com/problems/swim-in-rising-water/) - Hard

---

## Tags and Properties

- #dsa #important #revisit
- #graph [[Graph]] #dijkstra [[Dijkstra]] #shortestpath [[Shortest Path]] #priorityqueue [[Priority Queue]]
- **Date:** 2026-10-28
- **Problem Link:** [Network Delay Time - LeetCode](https://leetcode.com/problems/network-delay-time/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-10-30)
- [ ] Day 7 Revision (2026-11-04)
- [ ] Day 15 Revision (2026-11-12)
- [ ] Day 30 Revision (2026-11-27)
