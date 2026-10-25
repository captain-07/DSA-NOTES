---
created: 2026-09-24
revisions:
  - 2026-09-26
  - 2026-10-01
  - 2026-10-09
  - 2026-10-24
---

# Divide Intervals into Minimum Number of Groups

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:** #Amazon #Google #Microsoft #Meta #Uber
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]], #sorting [[Sorting]], #heaps [[Heaps]], #line-sweep [[Line Sweep]]

## Pattern

Line Sweep (Difference Array / Event Points) OR Min-Heap + Sorting

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

The minimum number of groups needed is equal to the **maximum number of overlapping intervals** at any point in time. We can process events (start/end) in chronological order or track group end times using a min-heap.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort start/end events (or end times in min-heap). Max concurrent overlapping intervals = minimum groups required.

---

## Approach

### Brute Force
- For each interval, check existing groups to see if it can fit without overlap; if not, create a new group.
- Time: $O(N^2)$, Space: $O(N)$

### Optimal 1: Min-Heap + Sorting
1. Sort intervals by start time.
2. Use a min-heap to store the end times of active groups.
3. For each interval, if `start_time > min_heap[0]` (smallest end time), reuse that group (pop heap).
4. Push current interval's end time to heap. Heap size at end is the result.

### Optimal 2: Line Sweep (Chronological Events)
1. Split each interval `[start, end]` into two events: `(start, +1)` and `(end + 1, -1)`.
2. Sort all events by time. If times tie, process `-1` (end) before `+1` (start).
3. Sweep through events maintaining a running count of active intervals. Peak count is the result.

### Optimal 3: Two Pointers on Sorted Starts / Ends
1. Extract all `start` times and all `end` times into two separate arrays and sort both.
2. Use `start_ptr` and `end_ptr`, tracking `active_groups` and `max_groups`.
3. If `starts[start_ptr] <= ends[end_ptr]`, an interval begins before another ends → increment `active_groups` and advance `start_ptr`.
4. Otherwise an interval has ended → decrement `active_groups` and advance `end_ptr`.
5. Return the maximum `active_groups` seen (equivalent to peak overlap).

---

## Code (Python)

```python
import heapq

class Solution:
    def minGroups(self, intervals: list[list[int]]) -> int:
        # Sort intervals primarily by start time
        intervals.sort(key=lambda x: x[0])

        # Min-heap to keep track of the end times of each group
        min_heap = []

        for start, end in intervals:
            # If the earliest ending group ends before current start, reuse it
            if min_heap and min_heap[0] < start:
                heapq.heappop(min_heap)

            # Add current interval's end time to the heap
            heapq.heappush(min_heap, end)

        # The number of elements in the heap represents total groups needed
        return len(min_heap)


class SolutionTwoPointers:
    def minGroups(self, intervals: list[list[int]]) -> int:
        # Extract and sort start and end points independently
        start_times = sorted([interval[0] for interval in intervals])
        end_times = sorted([interval[1] for interval in intervals])

        start_ptr = 0
        end_ptr = 0
        active_groups = 0
        max_groups = 0

        # Traverse chronologically through all start times
        while start_ptr < len(intervals):
            # Inclusive condition: an interval starting at/before another's end needs a new group
            if start_times[start_ptr] <= end_times[end_ptr]:
                active_groups += 1
                max_groups = max(max_groups, active_groups)
                start_ptr += 1
            else:
                active_groups -= 1
                end_ptr += 1

        return max_groups
```

---

## Dry Run (Smart Example)

Input: `intervals = [[5,10],[1,5],[5,6],[2,3],[5,10]]`
Sorted intervals: `[[1,5], [2,3], [5,6], [5,10], [5,10]]`

| Step | Current Interval `[start, end]` | `min_heap` Before | Action / Reason | `min_heap` After |
| :--- | :--- | :--- | :--- | :--- |
| 1 | `[1, 5]` | `[]` | Heap empty; add end `5` | `[5]` |
| 2 | `[2, 3]` | `[5]` | `start (2) <= min_heap[0] (5)` → cannot reuse group; push end `3` | `[3, 5]` |
| 3 | `[5, 6]` | `[3, 5]` | `start (5) > min_heap[0] (3)` → reuse group; pop `3`, push `6` | `[5, 6]` |
| 4 | `[5, 10]` | `[5, 6]` | `start (5) <= min_heap[0] (5)` → overlaps (starts at 5, previous ends at 5); push `10` | `[5, 6, 10]` |
| 5 | `[5, 10]` | `[5, 6, 10]` | `start (5) <= min_heap[0] (5)` → overlaps; push `10` | `[5, 6, 10, 10]` |

Result: `len(min_heap) = 4`

---

## Edge Cases

- **Intervals touching at boundary `[1,5]` and `[5,6]`:** Count as overlapping per problem description (requires strictly greater start time to reuse group).
- **Single interval `[[1,1]]`:** Returns `1`.
- **All intervals completely overlapping `[[1,10],[1,10]]`:** Returns number of intervals ($N$).
- **Disjoint intervals `[[1,2],[3,4],[5,6]]`:** Returns `1`.

---

## Mistakes

- **User Mistake:** Tried using two pointers approach (e.g., standard two-pointer array iteration without sorting events or maintaining dynamic end states fails because multiple active end times need constant tracking).
- Treating `start == end` as non-overlapping when the problem specifies intersection includes boundary points.
- Sorting only by end time instead of start time when using heap.

---

## Complexity

Time: $O(N \log N)$ → Sorting takes $O(N \log N)$, heap operations take $O(N \log N)$.
Space: $O(N)$ → Heap stores at most $N$ elements.

---

## Similar Problems

- [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) - Medium
- [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) - Medium
- [Car Pooling](https://leetcode.com/problems/car-pooling/) - Medium
- [Describe the Painting](https://leetcode.com/problems/describe-the-painting/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #intervals #heaps #sweep-line
- [[Sorting]], [[Heaps]], [[Line Sweep]]
- **Revision Date:** 2026-09-24
- **Problem Link:** [Divide Intervals Into Minimum Number Of Groups](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-26)
- [ ] Day 7 Revision (2026-10-01)
- [ ] Day 15 Revision (2026-10-09)
- [ ] Day 30 Revision (2026-10-24)
