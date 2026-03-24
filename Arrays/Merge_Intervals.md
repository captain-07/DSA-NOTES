---
created: 2026-03-23
revisions:
  - 2026-03-25
  - 2026-03-30
  - 2026-04-07
  - 2026-04-22
---

# Merge Intervals
---
## Difficulty
Medium
#medium
---
## Pattern
Greedy, Sorting
---
## Key Idea
The core intuition is that if we process the intervals in sorted order of their start times, we only need to consider if the current interval overlaps with the *most recently added* interval in our result set.
---
## Approach
**Brute Force:**
A naive approach would be to compare every interval with every other interval. Using two nested loops, if two intervals `i` and `j` are found to overlap, they are merged. This new merged interval then replaces one of the originals, and the other is marked for deletion. This process continues until no more merges can be made. This is highly inefficient, involving repeated comparisons and complex list management, leading to a complexity of at least $O(n^2)$.

**Optimal:**
The efficient approach leverages a greedy strategy.
1.  **Sort:** The first and most critical step is to sort the array of intervals based on their starting points. This ensures that we are processing intervals from left to right on the number line.
2.  **Initialize:** Create a result array (e.g., `merged_intervals`) and initialize it with the first interval from the sorted list.
3.  **Iterate and Merge:** Iterate through the sorted intervals, starting from the second one. For each `current_interval`:
    *   Let `last_merged` be the last interval in our `merged_intervals` result array.
    *   Check for overlap: If the `current_interval`'s start is less than or equal to the `last_merged`'s end (`current_interval[0] <= last_merged[1]`), they overlap.
    *   If they do overlap, we "merge" them by updating the end of `last_merged`. The new end will be the maximum of `last_merged`'s end and `current_interval`'s end. This handles cases where one interval is completely contained within another.
    *   If they do not overlap, the `current_interval` is distinct. We simply append it to our `merged_intervals` result array.
4.  **Return:** After the loop finishes, `merged_intervals` contains the final, non-overlapping set of intervals.
---
## Code
```python
def merge(intervals: list[list[int]]) -> list[list[int]]:
    # Edge case: if the list is empty or has one element, no merging is needed.
    if not intervals or len(intervals) == 1:
        return intervals

    # 1. Sort the intervals based on their start time.
    intervals.sort(key=lambda x: x[0])

    # 2. Initialize the result list with the first interval.
    merged = [intervals[0]]

    # 3. Iterate through the rest of the intervals.
    for i in range(1, len(intervals)):
        current_start, current_end = intervals[i]
        last_merged_start, last_merged_end = merged[-1]

        # 4. Check for overlap with the last interval in the result list.
        if current_start <= last_merged_end:
            # If they overlap, update the end of the last merged interval.
            # We take the max to handle contained intervals (e.g., [1,5] and [2,4]).
            merged[-1][1] = max(last_merged_end, current_end)
        else:
            # 5. If no overlap, it's a new interval. Append it.
            merged.append([current_start, current_end])
            
    return merged

```
---
## Dry Run
Let's trace with the input `intervals = [[1,4], [2,6], [8,10], [9,12]]`.

1.  **Sort:** The intervals are already sorted by their start times.
2.  **Initialize:** `merged = [[1, 4]]`

| Step | Current Interval (`intervals[i]`) | `merged[-1]` | Condition (`current[0] <= merged[-1][1]`) | Action | `merged` after step |
| :--- | :--- | :--- |:--- |:--- |:--- |
| 1 | `[2, 6]` | `[1, 4]` | `2 <= 4` (True) | Overlap. Update `merged[-1][1]` to `max(4, 6) = 6`. | `[[1, 6]]` |
| 2 | `[8, 10]` | `[1, 6]` | `8 <= 6` (False) | No overlap. Append `[8, 10]` to `merged`. | `[[1, 6], [8, 10]]` |
| 3 | `[9, 12]` | `[8, 10]` | `9 <= 10` (True) | Overlap. Update `merged[-1][1]` to `max(10, 12) = 12`. | `[[1, 6], [8, 12]]` |
| 4 | (End of loop) | - | - | - | `[[1, 6], [8, 12]]` |

**Final Result:** `[[1, 6], [8, 12]]`
---
## Edge Cases
1.  **Empty Input:** `intervals = []`. The code should handle this and return `[]`.
2.  **Single Interval:** `intervals = [[1, 5]]`. No merging is possible; it should return `[[1, 5]]`.
3.  **Contained Intervals:** `intervals = [[1, 10], [2, 6]]`. The `[2, 6]` interval is completely swallowed by `[1, 10]`. The result should be `[[1, 10]]`.
4.  **Adjacent Intervals:** `intervals = [[1, 5], [6, 10]]`. These do not overlap. The result should be `[[1, 5], [6, 10]]`.
---
## Mistakes
> [!CAUTION]
> **Common Gotchas & Errors**
> 1.  **Forgetting to Sort:** The entire greedy logic depends on processing intervals in increasing order of their start times. Skipping the sort step will lead to incorrect results.
> 2.  **Incorrect Merge Logic:** When merging, simply taking the second interval's end time is wrong. You must take the `max()` of the two intervals' end times. For example, merging `[1, 10]` and `[2, 6]` should result in `[1, 10]`, not `[1, 6]`.
> 3.  **Initializing with `if not ans`:** The user mentioned a mistake related to "appending first element by default using not ans". This initialization strategy is actually correct and common. The mistake is not the initialization itself, but rather what happens next. A common error is to then iterate from the *start* of the original list and compare `intervals[i]` with `intervals[i-1]`. This is wrong because `intervals[i-1]` might have already been merged into a larger interval. **The correct logic is to always compare the current interval with the *last element in the result list* (`merged[-1]`)**, not with its immediate predecessor in the original sorted list.
---
## Complexity
-   **Time Complexity:** $O(n \log n)$
    -   The complexity is dominated by the initial sorting of the intervals, which takes $O(n \log n)$ time. The subsequent single pass through the intervals takes $O(n)$ time.
-   **Space Complexity:** $O(n)$ or $O(\log n)$
    -   The space required for the output list is $O(n)$ in the worst case (if no intervals are merged). The space complexity of the sorting algorithm in Python (Timsort) is $O(n)$ in the worst case, but can be $O(\log n)$.
---
## Metadata & Placement Tags
-   **Companies:** #meta, #google, #amazon, #microsoft, #apple, #uber
-   **Confidence Level:** [ ] Low [ ] Mid [ ] High
-   **Concepts:** #greedy [[Greedy Algorithms]], #sorting [[Sorting]], #intervals [[Interval Problems]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-03-25)
- [ ] Day 7 Revision (2026-03-30)
- [ ] Day 15 Revision (2026-04-07)
- [ ] Day 30 Revision (2026-04-22)
