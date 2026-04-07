---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Single Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Uber #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #array [[Arrays]]
  - #bitmanipulation [[Bit Manipulation]]

---
## Pattern

Binary Search on Index Parity

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

In a paired sorted array, the "single" element disrupts the index parity. 
- **Left of Single Element:** Pairs follow `(Even Index, Odd Index)` pattern (e.g., `nums[i] == nums[i+1]` where `i` is even).
- **Right of Single Element:** Pairs follow `(Odd Index, Even Index)` pattern.
- **Goal:** Find the first index where this property breaks using Binary Search.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use `mid ^ 1` to find the partner index. If `nums[mid] == nums[mid ^ 1]`, the single element is on the **right**; otherwise, it's on the **left**.

---

## Approach

### Brute Force
- Linear scan through the array using a pointer or XORing all elements.
- **Complexity:** O(N) time, O(1) space.

### Better
- Check elements in pairs while iterating (skipping by 2).
- **Complexity:** O(N/2) time, O(1) space.

### Optimal
1. Initialize `low = 0` and `high = len(nums) - 2`.
2. While `low <= high`:
   - Calculate `mid`.
   - Use the **XOR Trick**: `mid ^ 1`. 
     - If `mid` is even, `mid ^ 1` is `mid + 1`.
     - If `mid` is odd, `mid ^ 1` is `mid - 1`.
   - If `nums[mid] == nums[mid ^ 1]`: We are in the left half; move `low = mid + 1`.
   - Else: We are in the right half or at the element; move `high = mid - 1`.
3. The answer is at `nums[low]`.

---

## Code (Python)

```python
def singleNonDuplicate(nums: list[int]) -> int:
    # Search space excludes the last element to avoid boundary checks
    low, high = 0, len(nums) - 2
    
    while low <= high:
        mid = (low + high) // 2
        
        # The XOR trick handles both even and odd mid parity
        # If mid is even, mid^1 is mid+1. If mid is odd, mid^1 is mid-1.
        if nums[mid] == nums[mid ^ 1]:
            # Property holds (Even-Odd pair), move right
            low = mid + 1
        else:
            # Property broken, single element is on the left
            high = mid - 1
            
    return nums[low]
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 1, 2, 3, 3, 4, 4]`

| Step | Low | High | Mid | mid ^ 1 | Comparison | Action |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 3 | `nums[2]=2 != nums[3]=3` | `high = mid - 1 = 1` |
| 2 | 0 | 1 | 0 | 1 | `nums[0]=1 == nums[1]=1` | `low = mid + 1 = 1` |
| 3 | 1 | 1 | 1 | 0 | `nums[1]=1 == nums[0]=1` | `low = mid + 1 = 2` |
| 4 | 2 | 1 | - | - | `low > high` | **Return nums[2] = 2** |

---

## Edge Cases

- **Array Size 1:** `[1]` → Handled by `low=0, high=-1`, returns `nums[0]`.
- **Single Element at End:** `[1, 1, 2, 2, 3]` → `low` will correctly increment to the last index.
- **Single Element at Start:** `[1, 2, 2, 3, 3]` → `high` will correctly decrement until `low=0`.
- **All elements identical except one:** Standard case.

---

## Mistakes

- **User Mistake:** Manually checking `if mid % 2 == 0` and comparing with `mid + 1` or `mid - 1`. This leads to verbose, error-prone boundary checks.
- Using `high = len(nums) - 1` and forgetting to handle index out of bounds for `mid + 1`.
- Not realizing the array must be sorted for the $O(\log N)$ approach.

---

## Complexity

Time: O(log N) → Binary search halves the search space each step.  
Space: O(1) → Constant space used for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Find Peak Element](https://leetcode.com/problems/find-peak-element/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #logic
  - [[Binary Search]] [[Bit Manipulation]]
  - **Revision Date:** 2026-04-07
  - **Problem Link:** [LeetCode - Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
