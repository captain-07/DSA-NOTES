---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Single Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]], #array [[Array]], #bitmanipulation [[Bit Manipulation]]

## Pattern

Binary Search (Index Parity)

---
## Difficulty

Medium #medium

---

## ⚡ Key Idea (Core Insight)

In a sorted array where every element appears twice except one, pairs before the single element always follow an **(even, odd)** index pattern (e.g., indices 0 & 1, 2 & 3). After the single element, the pattern shifts to **(odd, even)**. We use Binary Search to find the point where this pattern breaks.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use `nums[mid] == nums[mid ^ 1]` to stay in the left half. If true, the single element is to the right; if false, it is to the left or at `mid`.

---

## Approach

### Brute Force
- XOR all elements in the array. Since $x \oplus x = 0$, all pairs cancel out, leaving the single element.
- **Time:** O(N)
- **Space:** O(1)

### Better
- Linear scan with a step of 2, checking if `nums[i] == nums[i+1]`. The first index `i` where this fails is the start of the single element.
- **Time:** O(N)
- **Space:** O(1)

### Optimal
1. Initialize `low = 0` and `high = n - 2` (to avoid boundary checks on the last element).
2. Calculate `mid`.
3. Check if `nums[mid]` is equal to its intended partner using the XOR trick: `mid ^ 1`.
   - If `mid` is even: `mid ^ 1` is `mid + 1`.
   - If `mid` is odd: `mid ^ 1` is `mid - 1`.
4. If `nums[mid] == nums[mid ^ 1]`, we are in the left half; move `low = mid + 1`.
5. Otherwise, we are in the right half; move `high = mid - 1`.
6. After the loop, `nums[low]` is the single element.

---

## Code (Python)

```python
class Solution:
    def singleNonDuplicate(self, nums: list[int]) -> int:
        # We search in the range [0, n-2] to find the first transition
        low, high = 0, len(nums) - 2
        
        while low <= high:
            mid = (low + high) // 2
            
            # The XOR Trick:
            # If mid is even, mid ^ 1 = mid + 1
            # If mid is odd,  mid ^ 1 = mid - 1
            # This check determines if we are in the 'left' side (even, odd)
            if nums[mid] == nums[mid ^ 1]:
                # Pattern holds, single element must be on the right
                low = mid + 1
            else:
                # Pattern broken, single element is here or to the left
                high = mid - 1
        
        # 'low' will always point to the single element
        return nums[low]
```

---

## Dry Run (Smart Example)

Input: `nums = [1, 1, 2, 2, 3, 4, 4]` (Single element is 3 at index 4)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `low=0, high=5, mid=2` | `mid^1=3`. `nums[2]=2, nums[3]=2`. Match! `low = 3`. |
| 2 | `low=3, high=5, mid=4` | `mid^1=5`. `nums[4]=3, nums[5]=4`. No Match! `high = 3`. |
| 3 | `low=3, high=3, mid=3` | `mid^1=2`. `nums[3]=2, nums[2]=2`. Match! `low = 4`. |
| 4 | `low=4, high=3` | Loop terminates. Return `nums[4]` which is `3`. |

---

## Edge Cases

- **Single Element Array:** `[1]` → `low=0, high=-1`, loop skipped, returns `nums[0]`.
- **Single Element at Start:** `[1, 2, 2]` → `mid=0, nums[0]!=nums[1]`, `high=-1`, returns `nums[0]`.
- **Single Element at End:** `[1, 1, 2]` → `mid=0, nums[0]==nums[1]`, `low=1`, `mid=1, nums[1]==nums[0]`, `low=2`, returns `nums[2]`.

---

## Mistakes

- Using XOR `O(N)` solution when the problem specifically asks for `O(log N)` (usually implied by "sorted").
- Overcomplicating boundaries by manually checking `if mid % 2 == 0`.
- **User Mistake:** Manually checking `if mid % 2 == 0` and comparing with `mid + 1` or `mid - 1`. This leads to verbose, error-prone boundary checks. Use the `mid ^ 1` idiom instead.

---

## Complexity

Time: O(log N) → Reducing search space by half in each iteration.  
Space: O(1) → Constant space for pointers.

---

## Similar Problems

- [Search in Rotated Sorted Array](https://leetcode.com/problems/search-in-rotated-sorted-array/) - Medium
- [Find Minimum in Rotated Sorted Array](https://leetcode.com/problems/find-minimum-in-rotated-sorted-array/) - Medium
- [Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/) - Medium

---

## Tags and Properties
  - #dsa #important #revisit #binarysearch #array
  - [[Binary Search]] [[Array]]
  - **Revision Date:** 2026-04-10
  - **Problem Link:** [LeetCode - Single Element in a Sorted Array](https://leetcode.com/problems/single-element-in-a-sorted-array/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
