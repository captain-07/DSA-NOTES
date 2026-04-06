---
created: 2026-04-06
revisions:
  - 2026-04-08
  - 2026-04-13
  - 2026-04-21
  - 2026-05-06
---

# Find Peak Element

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Uber #LinkedIn

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Arrays]]

## Pattern

Modified Binary Search (Binary Search on Slope/Answer)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

A peak element must exist in any array where `nums[-1] = nums[n] = -∞`. We use **Binary Search** to find the "ascending" slope. If `nums[mid] < nums[mid + 1]`, we are on an upward slope, so a peak *must* exist to the right. Otherwise, a peak exists at `mid` or to the left.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Compare `nums[mid]` with `nums[mid + 1]`. If increasing, move `left = mid + 1`. If decreasing, move `right = mid`.

---

## Approach

### Brute Force
- Linear scan through the array to find the first element that is greater than its neighbors.
- **Time Complexity:** O(n)

### Optimal (Binary Search)
1. Initialize `left = 0`, `right = n - 1`.
2. While `left < right`:
   - Calculate `mid`.
   - If `nums[mid] < nums[mid + 1]`: We are climbing; move `left = mid + 1`.
   - Else: We are descending or at a peak; move `right = mid`.
3. Return `left` (or `right`), as they converge on a peak.

---

## Code (Python)

```python
def findPeakElement(nums):
    left, right = 0, len(nums) - 1
    
    while left < right:
        mid = (left + right) // 2
        
        # If mid is less than the next element, peak is on the right
        if nums[mid] < nums[mid + 1]:
            left = mid + 1
        # If mid is greater than next, mid could be the peak or peak is on the left
        else:
            right = mid
            
    return left  # left and right converge to the peak index
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 2, 1, 3, 5, 6, 4]`

| Step | left | right | mid | nums[mid] vs nums[mid+1] | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 6 | 3 | 3 < 5 (Increasing) | left = 4 |
| 2 | 4 | 6 | 5 | 6 > 4 (Decreasing) | right = 5 |
| 3 | 4 | 5 | 4 | 5 < 6 (Increasing) | left = 5 |
| 4 | 5 | 5 | - | Loop Ends (left == right) | Return 5 |

**Result:** Index 5 (Value 6) is a peak.

---

## Edge Cases

- **Single Element:** `[1]` → Loop doesn't run, returns index 0.
- **Strictly Increasing:** `[1, 2, 3]` → Always moves `left`, returns last index.
- **Strictly Decreasing:** `[3, 2, 1]` → Always moves `right`, returns index 0.
- **Two Elements:** `[1, 2]` → `mid` is 0, `nums[0] < nums[1]`, returns index 1.

---

## Mistakes

- Using `left <= right` which can cause an infinite loop or index out of bounds when checking `mid + 1`.
- Not recognizing that $O(\log n)$ requirement mandates a Binary Search approach even on unsorted data.
- User mistake: No specific note provided.

---

## Complexity

Time: O(log N) → We reduce the search space by half in each iteration.  
Space: O(1) → Only constant extra space used for pointers.

---

## Tags and Properties

- #dsa #important #revisit #leetcode162
- [[Binary Search]] [[Arrays]]
- Revision Date: 2026-04-06
- Related: [[Find Minimum in Rotated Sorted Array]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-08)
- [ ] Day 7 Revision (2026-04-13)
- [ ] Day 15 Revision (2026-04-21)
- [ ] Day 30 Revision (2026-05-06)
