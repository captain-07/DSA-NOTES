---
created: 2026-04-07
revisions:
  - 2026-04-09
  - 2026-04-14
  - 2026-04-22
  - 2026-05-07
---

# Reverse An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]], #twopointers [[Two Pointers]], #inplace [[In-place Algorithms]]

---
## Pattern

Two Pointers (Opposite Ends)

---
## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

The symmetry of an array allows us to swap elements from the outside-in. By maintaining two pointers at the boundaries, we can transform the array in-place without requiring extra memory.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Swap `arr[left]` with `arr[right]`, increment `left`, decrement `right`, repeat until they meet.

---

## Approach

### Brute Force
- Create a new array of the same size. Iterate through the original array from last to first and copy elements into the new array.
- **Time:** O(N)
- **Space:** O(N)

### Better (Recursive)
- Swap the first and last elements, then recursively call the function for the remaining subarray.
- **Time:** O(N)
- **Space:** O(N) due to recursion stack.

### Optimal (Two Pointers)
1. Initialize `left = 0` and `right = len(arr) - 1`.
2. While `left < right`:
   - Swap `arr[left]` and `arr[right]`.
   - `left += 1`
   - `right -= 1`
3. The array is reversed in-place.

---

## Code (Python)

```python
def reverse_array(arr):
    # Initialize pointers at both ends
    left = 0
    right = len(arr) - 1
    
    # Continue swapping until pointers meet in the middle
    while left < right:
        # Pythonic swap: no temp variable needed
        arr[left], arr[right] = arr[right], arr[left]
        
        # Move pointers towards the center
        left += 1
        right -= 1
        
    return arr
```

---

## Dry Run (Smart Example)

**Input:** `arr = [10, -5, 30, 10, 50]` (Odd length, negatives, and duplicates)

| Step | Pointers (L, R) | Variables (`arr[L]`, `arr[R]`) | Explanation | Resulting Array |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 0, 4 | 10, 50 | Swap indices 0 and 4 | `[50, -5, 30, 10, 10]` |
| 2 | 1, 3 | -5, 10 | Swap indices 1 and 3 | `[50, 10, 30, -5, 10]` |
| 3 | 2, 2 | 30, 30 | `L == R`, Loop terminates | `[50, 10, 30, -5, 10]` |

---

## Edge Cases

- **Empty Array:** Loop condition `left < right` (0 < -1) is false; returns `[]` correctly.
- **Single Element:** `left == right` initially; no swaps occur.
- **Even Length:** Pointers cross perfectly (e.g., `L=2, R=3` then `L=3, R=2`).
- **Already Sorted/Reversed:** Logic remains identical and correct.

---

## Mistakes

- **Reversing Entirely Twice:** Using a `for i in range(len(arr))` loop without stopping at the middle results in the original array.
- **Off-by-one Error:** Initializing `right = len(arr)` instead of `len(arr) - 1`.
- **Inefficient Slicing:** Using `arr[::-1]` is concise but creates a copy (O(N) space); avoid if in-place is required.
- **User Mistake:** None.

---

## Complexity

- **Time:** O(N) → We visit each element exactly once (N/2 swaps).
- **Space:** O(1) → Swapping is done in-place without extra data structures.

---

## Similar Problems

- [Reverse String](https://leetcode.com/problems/reverse-string/) - Easy
- [Reverse Vowels of a String](https://leetcode.com/problems/reverse-vowels-of-a-string/) - Easy
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
- [Rotate Array](https://leetcode.com/problems/rotate-array/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #arrays #twopointers [[Arrays]] [[Two Pointers]]
- **Revision Date:** 2026-04-07
- **Problem Link:** [LeetCode - Reverse String (Array Variant)](https://leetcode.com/problems/reverse-string/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-09)
- [ ] Day 7 Revision (2026-04-14)
- [ ] Day 15 Revision (2026-04-22)
- [ ] Day 30 Revision (2026-05-07)
