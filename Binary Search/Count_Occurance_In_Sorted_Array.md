---
created: 2026-04-11
revisions:
  - 2026-04-13
  - 2026-04-18
  - 2026-04-26
  - 2026-05-11
---

# Count Occurance In Sorted Array

---

## Pattern

Binary Search (Boundary Finding)

---
## Difficulty

Easy | #easy

---

## ⚡ Key Idea (Core Insight)

- In a sorted array, the count of a target is the distance between its **first** and **last** occurrence.
- Both boundaries can be found in $O(\log N)$ using modified Binary Search.
- `Count = (Last Index - First Index + 1)` if the element exists, else `0`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- Perform two Binary Searches: one for the leftmost (lower bound) and one for the rightmost (upper bound). Result is `last_idx - first_idx + 1`.

---

## Approach

### Brute Force
- Linear scan through the array to count occurrences of the target.
- **Time Complexity:** $O(N)$
- **Space Complexity:** $O(1)$

### Optimal
- Use two binary search functions: `findFirst` and `findLast`.
- **Logic for `findFirst`**: When `nums[mid] == target`, save the index and move `high = mid - 1` to search for an earlier occurrence.
- **Logic for `findLast`**: When `nums[mid] == target`, save the index and move `low = mid + 1` to search for a later occurrence.
- **Time Complexity:** $O(\log N)$

---

## Code (Python)

```python
class Solution:
    def countOccurrences(self, nums: list[int], target: int) -> int:
        def find_bound(is_first: bool) -> int:
            low, high = 0, len(nums) - 1
            bound = -1
            while low <= high:
                mid = (low + high) // 2
                if nums[mid] == target:
                    bound = mid
                    if is_first:
                        high = mid - 1 # Search Left
                    else:
                        low = mid + 1  # Search Right
                elif nums[mid] < target:
                    low = mid + 1
                else:
                    high = mid - 1
            return bound

        first = find_bound(True)
        if first == -1: return 0 # Target not found
        
        last = find_bound(False)
        return last - first + 1

    # Alternative: Using Python's built-in bisect
    def countWithBisect(self, nums: list[int], target: int) -> int:
        import bisect
        left = bisect.bisect_left(nums, target)
        right = bisect.bisect_right(nums, target)
        return right - left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 1, 2, 2, 2, 2, 3], target = 2`

| Step | Action | Variables | Explanation |
| :--- | :--- | :--- | :--- |
| 1 | Find First | `low=0, high=6, mid=3` | `nums[3]=2`. `bound=3`, search left: `high=2`. |
| 2 | Find First | `low=0, high=2, mid=1` | `nums[1]=1`. Search right: `low=2`. |
| 3 | Find First | `low=2, high=2, mid=2` | `nums[2]=2`. `bound=2`, search left: `high=1`. Exit. |
| 4 | Find Last | `low=0, high=6, mid=3` | `nums[3]=2`. `bound=3`, search right: `low=4`. |
| 5 | Find Last | `low=4, high=6, mid=5` | `nums[5]=2`. `bound=5`, search right: `low=6`. |
| 6 | Result | `5 - 2 + 1` | `4` occurrences found. |

---

## Edge Cases

- **Target not present:** Binary search returns `-1`, resulting in `0`.
- **Empty array:** Loop never executes, returns `0`.
- **All elements are target:** Correctly returns `len(nums)`.
- **Target at boundaries:** Correctly identifies index `0` or `n-1`.

---

## Mistakes

- **Sub-optimal approach:** Using linear scan $O(N)$ instead of taking advantage of the sorted property.
- **Stopping early:** Returning after finding the first `mid` that matches without searching for range.
- **Handling -1:** Not checking if the first occurrence exists before calculating the range.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(log N) → Two binary search passes take logarithmic time.  
Space: O(1) → Constant space used for pointers.

---

## Similar Problems

- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium
- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Binary Search](https://leetcode.com/problems/binary-search/) - Easy
- [Search Insert Position](https://leetcode.com/problems/search-insert-position/) - Easy

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #array #sorting
  - [[Binary Search]] [[Array]] [[Sorting]]
  - **Revision Date:** 2026-04-11
  - **Problem Link:** [Count occurrences of a number in a sorted array - GeeksforGeeks](https://www.geeksforgeeks.org/problems/count-occurences-of-number-in-sorted-array4751/1)

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Samsung #Walmart #Flipkart
- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]], #sorting [[Sorting]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-13)
- [ ] Day 7 Revision (2026-04-18)
- [ ] Day 15 Revision (2026-04-26)
- [ ] Day 30 Revision (2026-05-11)
