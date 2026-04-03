---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Search Insert Position

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #Apple #Facebook #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #searching [[Searching]]

---
## Pattern

Binary Search (Finding Lower Bound / Insertion Point)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The problem asks for the index of the target or the index where it *would* be. In a sorted array, standard **Binary Search** naturally terminates with the `left` pointer sitting at the first element greater than the target, which is exactly the insertion index.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Perform Binary Search. If the target is not found, the `left` pointer is the answer.

---

## Approach

### Brute Force
- Linear search through the array. Return the index `i` where `nums[i] >= target`.
- **Time:** $O(n)$

### Optimal (Iterative Binary Search)
1. Initialize `left = 0` and `right = len(nums) - 1`.
2. While `left <= right`:
   - Calculate `mid = (left + right) // 2`.
   - If `nums[mid] == target`, return `mid`.
   - If `nums[mid] < target`, move `left = mid + 1`.
   - Else, move `right = mid - 1`.
3. If loop finishes, return `left`.
- **Time:** $O(\log n)$

### Optimal (Pythonic Library)
- Use `bisect.bisect_left(nums, target)`.
- This finds the leftmost insertion point to maintain order.
- **Time:** $O(\log n)$

---

## Code (Python)

```python
def searchInsert(nums, target):
    left, right = 0, len(nums) - 1
    
    while left <= right:
        # Standard mid calculation
        mid = left + (right - left) // 2
        
        if nums[mid] == target:
            return mid
        elif nums[mid] < target:
            left = mid + 1
        else:
            right = mid - 1
            
    # If not found, 'left' is the insertion index
    return left
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 3, 5, 6]`, `target = 2`

| Step | Left | Right | Mid | nums[mid] | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 3 | 1 | 3 | `3 > 2` → `right = mid - 1 = 0` |
| 2 | 0 | 0 | 0 | 1 | `1 < 2` → `left = mid + 1 = 1` |
| 3 | 1 | 0 | - | - | `left > right` → **Terminate** |

**Result:** Return `left = 1`.

---

## Edge Cases

- **Target smaller than all:** `nums = [1, 3, 5], target = 0`. Returns index `0`.
- **Target larger than all:** `nums = [1, 3, 5], target = 10`. Returns index `3` (len).
- **Array size 1:** `nums = [1], target = 2`. Returns index `1`.
- **Target already exists:** Returns the actual index of the target.

---

## Mistakes

- **Incorrect Loop Condition:** Using `left < right` instead of `left <= right` can miss the last element check.
- **Mid Overflow:** Using `(left + right) // 2` in languages with fixed integer sizes (use `left + (right-left)//2`).
- **Returning wrong pointer:** Returning `right` or `mid` instead of `left` on a miss.
- **User Mistake:** No specific note provided. (Ensure you document the insertion logic clearly).

---

## Complexity

- **Time:** $O(\log n)$ → Range is halved in every iteration of the binary search.
- **Space:** $O(1)$ → Only pointers/variables are used; no extra data structures.

---

## Tags and Properties
- #dsa #important #revisit #searching #binarysearch
- [[Binary Search]] [[Arrays]]
- Revision Date: 2026-04-03
- Related: [[Search in Rotated Sorted Array]], [[First and Last Position of Element]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
