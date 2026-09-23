---
created: 2026-09-23
revisions:
  - 2026-09-25
  - 2026-09-30
  - 2026-10-08
  - 2026-10-23
---

# Non-Overlapping Intervals

---

## Metadata & Placement Tags

- **Folder:** Greedy
- **Target Companies:** #Amazon #Facebook #Microsoft #Google #Apple
- **Confidence Checklist:**
  - [ ] Low
  - [ ] Medium
  - [ ] High

- **Concepts:**
  - #greedy [[Greedy]], #sorting [[Sorting]], #intervals [[Intervals]]

## Pattern

Sorting + Greedy (Interval Scheduling)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

To minimize removals, greedily pick intervals that end as early as possible. Sorting by end time leaves maximum room for subsequent intervals, avoiding overlaps.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Sort by **end time**. Keep track of the end time of the last non-overlapping interval. If current `start < last_end`, increment remove count; else update `last_end = end`.

---

## Approach

### Brute Force
- Generate all possible subsets of intervals and check if any contain overlapping intervals. Find the largest valid subset and subtract its size from total intervals.
- **Time Complexity:** $O(2^N \cdot N)$

### Optimal
- Sort intervals by their ending times.
- Iterate through intervals maintaining `last_end`.
- If `start < last_end`, we must remove current interval (increment count).
- Otherwise, update `last_end = end`.
- **Time Complexity:** $O(N \log N)$

---

## Code (Python)

```python
class Solution:
    def eraseOverlapIntervals(self, intervals: list[list[int]]) -> int:
        if not intervals:
            return 0

        # Sort intervals based on their end times
        intervals.sort(key=lambda x: x[1])

        count_removed = 0
        last_end_time = intervals[0][1]

        # Iterate from the second interval onwards
        for i in range(1, len(intervals)):
            current_start = intervals[i][0]
            current_end = intervals[i][1]

            # If overlap occurs with previous selected interval
            if current_start < last_end_time:
                count_removed += 1
            else:
                # Update end time to current non-overlapping interval's end time
                last_end_time = current_end

        return count_removed
```

---

## Dry Run (Smart Example)

Input: `intervals = [[1, 100], [11, 22], [1, 11], [2, 12]]`
Sorted by End Time: `[[1, 11], [2, 12], [11, 22], [1, 100]]`

| Step | Variables | Explanation |
|---|---|---|
| 0 | `last_end = 11`, `count = 0` | Pick first interval `[1, 11]`. |
| 1 | `curr = [2, 12]` | `start (2) < last_end (11)` $\rightarrow$ Overlap! Increment `count = 1`. |
| 2 | `curr = [11, 22]` | `start (11) >= last_end (11)` $\rightarrow$ No overlap. Update `last_end = 22`. |
| 3 | `curr = [1, 100]` | `start (1) < last_end (22)` $\rightarrow$ Overlap! Increment `count = 2`. |

**Result:** `2` removals needed.

---

## Edge Cases

- **Empty or single interval:** Return 0 immediately.
- **Intervals touching at endpoints (e.g., `[1, 2]` & `[2, 3]`):** Not considered overlapping.
- **Identical intervals:** Force removal of duplicates.
- **Negative coordinates (e.g., `[-50, -20]`, `[-30, -10]`):** Sorting correctly handles negative numbers.

---

## Mistakes

- Sorting by start time instead of end time (requires additional tricky logic).
- Treating touching boundaries (e.g., `start == end`) as overlapping (`start < last_end` vs `start <= last_end`).
- User Mistake: No specific note provided.

---

## Complexity

Time: $O(N \log N)$ → Dominated by sorting $N$ intervals.
Space: $O(1)$ or $O(N)$ → Dependent on the space complexity of Python's Timsort algorithm.

---

## Similar Problems

- [Merge Intervals](https://leetcode.com/problems/merge-intervals/) - Medium
- [Insert Interval](https://leetcode.com/problems/insert-interval/) - Medium
- [Minimum Number of Arrows to Burst Balloons](https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/) - Medium
- [Meeting Rooms II](https://leetcode.com/problems/meeting-rooms-ii/) - Medium

---

## Tags and Properties

- #dsa #important #revisit #greedy #sorting #intervals
- [[Greedy Algorithm]] [[Interval Scheduling]] [[Sorting]]
- **Revision Date:** 2026-09-23
- **Problem Link:** [LeetCode - Non-Overlapping Intervals](https://leetcode.com/problems/non-overlapping-intervals/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-09-25)
- [ ] Day 7 Revision (2026-09-30)
- [ ] Day 15 Revision (2026-10-08)
- [ ] Day 30 Revision (2026-10-23)
