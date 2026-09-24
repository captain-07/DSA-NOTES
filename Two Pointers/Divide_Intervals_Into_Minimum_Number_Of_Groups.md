---
created: 2026-09-24
revisions:
  - 2026-09-26
  - 2026-10-01
  - 2026-10-09
  - 2026-10-24
---

# Divide Intervals Into Minimum Number Of Groups

---

## Metadata & Placement Tags

- **Folder:** Two Pointers
- **Target Companies:**
  - #Google #Amazon #Microsoft #Bloomberg #Meta
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High
- **Concepts:**
  - #twopointers [[Two Pointers]], #sorting [[Sorting]], #greedy [[Greedy]], #heaps [[Heaps]]

## Pattern

Two Pointers + Sorting (Chronological Events / Sweep Line)

---
## Difficulty

Medium
#medium

---

## ⚡ Key Idea (Core Insight)

The minimum number of groups required equals the **maximum number of overlapping intervals** at any single point in time. Each overlap at the same time requires a distinct group.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort `start` and `end` times independently. Use two pointers to simulate chronological arrival and departure; count active concurrent intervals (`start <= end` increments count, else decrements).

---

## Approach

### Brute Force
- Check every integer point covered by intervals and count overlaps by iterating over all intervals.
- Time Complexity: $O(N \times \text{Range})$

### Better (Min-Heap)
- Sort intervals by start time; push end times into a min-heap. If current `start > heap[0]`, pop the root (reuse group), then push current `end`.
- Time Complexity: $O(N \log N)$, Space: $O(N)$

### Optimal (Two Pointers / Chronological Events)
1. Extract all `start` times and `end` times into two separate arrays and sort both.
2. Initialize two pointers: `start_ptr = 0`, `end_ptr = 0`, tracking `active_groups = 0` and `max_groups = 0`.
3. If `start[start_ptr] <= end[end_ptr]`, an interval begins before another ends $\rightarrow$ increment `active_groups` and advance `start_ptr`.
4. Otherwise, an interval has ended $\rightarrow$ decrement `active_groups` and advance `end_ptr`.
5. Return the maximum `active_groups` encountered.

---

## Code (Python)

```python
class Solution:
    def minGroups(self, intervals: list[list[int]]) -> int:
        # Extract and sort start and end points independently
        start_times = sorted([interval[0] for interval in intervals])
        end_times = sorted([interval[1] for interval in intervals])

        start_ptr = 0
        end_ptr = 0
        active_groups = 0
        max_groups = 0

        total_intervals = len(intervals)

        # Traverse chronologically through all start times
        while start_ptr < total_intervals:
            # Inclusive condition: if an interval starts before or at the end of another
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

**Input:** `intervals = [[5, 10], [6, 8], [1, 5], [2, 3]]`
`start_times = [1, 2, 5, 6]`, `end_times = [3, 5, 8, 10]`

| Step | Variables (`start_ptr`, `end_ptr`, `active_groups`) | Explanation |
| :--- | :--- | :--- |
| 1 | `start_ptr=0` (1), `end_ptr=0` (3), `active=1` | `1 <= 3` $\rightarrow$ Interval starts. `active=1`, `max_groups=1`. Advance `start_ptr`. |
| 2 | `start_ptr=1` (2), `end_ptr=0` (3), `active=2` | `2 <= 3` $\rightarrow$ Interval starts. `active=2`, `max_groups=2`. Advance `start_ptr`. |
| 3 | `start_ptr=2` (5), `end_ptr=0` (3), `active=1` | `5 > 3` $\rightarrow$ Interval ends. `active=1`. Advance `end_ptr`. |
| 4 | `start_ptr=2` (5), `end_ptr=1` (5), `active=2` | `5 <= 5` (inclusive overlap) $\rightarrow$ New interval starts before prev clears. `active=2`, `max_groups=2`. Advance `start_ptr`. |
| 5 | `start_ptr=3` (6), `end_ptr=1` (5), `active=1` | `6 > 5` $\rightarrow$ Interval ends. `active=1`. Advance `end_ptr`. |
| 6 | `start_ptr=3` (6), `end_ptr=2` (8), `active=2` | `6 <= 8` $\rightarrow$ Interval starts. `active=2`, `max_groups=2`. Advance `start_ptr`. |

**Result:** `2`

---

## Edge Cases

- **Single interval:** `[[1, 1]]` $\rightarrow$ Returns `1`.
- **Touching endpoints (inclusive):** `[[1, 5], [5, 10]]` $\rightarrow$ Overlaps at `5`, requires `2` groups (`start <= end` handles this).
- **All disjoint intervals:** `[[1, 2], [3, 4], [5, 6]]` $\rightarrow$ Returns `1`.
- **All identical intervals:** `[[2, 4], [2, 4], [2, 4]]` $\rightarrow$ Returns `3`.

---

## Mistakes

- User Mistake: Forgetting that two pointers on sorted start and end arrays provides the cleanest $O(N \log N)$ chronological events approach without needing extra event tags (+1/-1 tuples).
- Using `<` instead of `<=` when checking `start <= end`, failing to account for inclusive endpoints overlapping.
- Trying to track which specific interval belongs to which group instead of realizing the answer is simply the maximum concurrent overlap count.

---

## Complexity

Time: $O(N \log N)$ → Sorting start and end time arrays dominates the two-pointer traversal.
Space: $O(N)$ → Storing separated start and end time arrays.

---

## Similar Problems

- [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) - Medium
- [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) - Medium
- [Car Pooling](https://leetcode.com/problems/car-pooling/) - Medium
- [Corporate Flight Bookings](https://leetcode.com/problems/corporate-flight-bookings/) - Medium

---

## Tags and Properties

- #dsa #important #revisit
- #intervals #sweepline #twopointers #sorting
- Concepts: [[Two Pointers]], [[Sorting]], [[Greedy]], [[Sweep Line]]
- Revision Date: 2026-09-24
- **Problem Link:** [LeetCode - Divide Intervals Into Minimum Number of Groups](https://leetcode.com/problems/divide-intervals-into-minimum-number-of-groups/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-26)
- [ ] Day 7 Revision (2026-10-01)
- [ ] Day 15 Revision (2026-10-09)
- [ ] Day 30 Revision (2026-10-24)
