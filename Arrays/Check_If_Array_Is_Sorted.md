---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Check If Array Is Sorted

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #TCS #Infosys #Wipro

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [x] High  

- **Concepts:**
  - #array [[Array]]
  - #traversal [[Linear Traversal]]

---
## Pattern

Linear Traversal (Single Pass)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

An array is sorted (non-decreasing) if and only if **every** element is less than or equal to the element following it: `arr[i] <= arr[i+1]`. A single violation of this property immediately invalidates the sorted status.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Iterate from `0` to `n-2`. If `arr[i] > arr[i+1]`, return `False`. If the loop finishes, return `True`.

---

## Approach

### Brute Force
- Compare every element with every other element that comes after it.
- Time Complexity: O(N²)
- Space Complexity: O(1)

### Optimal
- Perform a single linear scan through the array.
- Compare adjacent pairs: `(arr[0], arr[1]), (arr[1], arr[2]), ...`
- Time Complexity: O(N)
- Space Complexity: O(1)

---

## Code (Python)

```python
class Solution:
    def isSorted(self, arr: list[int]) -> bool:
        """
        Checks if the array is sorted in non-decreasing order.
        """
        n = len(arr)
        
        # Edge case: Empty or single-element arrays are sorted
        if n <= 1:
            return True
            
        for i in range(n - 1):
            # If current element is greater than next, it's not sorted
            if arr[i] > arr[i + 1]:
                return False
        
        return True
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, 2, 4, 3, 5]`

| Step | `i` | `arr[i]` vs `arr[i+1]` | Explanation | Result |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | `1 <= 2` | Condition holds. | Continue |
| 2 | 1 | `2 <= 4` | Condition holds. | Continue |
| 3 | 2 | `4 > 3` | **Violation found!** | **Return False** |

---

## Edge Cases

- **Empty Array `[]`:** Should return `True` (vacuously sorted).
- **Single Element `[5]`:** Should return `True`.
- **All Identical Elements `[2, 2, 2]`:** Should return `True` (non-decreasing).
- **Strictly Decreasing `[5, 4, 3]`:** Should return `False`.
- **Unsorted at the very end `[1, 2, 3, 0]`:** Ensures the loop covers all adjacent pairs.

---

## Mistakes

- **Index Out of Bounds:** Running the loop to `n` instead of `n-1` when checking `arr[i+1]`.
- **Wrong Comparison:** Using `<` instead of `<=` (ignoring duplicate elements).
- **Premature Return:** Returning `True` inside the loop after the first successful comparison instead of waiting for the loop to complete.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Must visit each element at most once to verify order.  
Space: O(1) → No extra data structures used; only a pointer/index.

---

## Similar Problems

- [Check if Array Is Sorted and Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/) - Easy
- [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) - Easy
- [Find the Second Largest Element in an Array](https://www.geeksforgeeks.org/problems/second-largest3735/1) - Easy

---

## Tags and Properties
  - #dsa #important #revisit  
  - #arrays #sorting [[Sorting]] #basics
  - **Revision Date:** 2026-04-25
  - **Problem Link:** [LeetCode - Check if Array Is Sorted and Rotated](https://leetcode.com/problems/check-if-array-is-sorted-and-rotated/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
