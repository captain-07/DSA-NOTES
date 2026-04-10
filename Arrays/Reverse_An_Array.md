---
created: 2026-04-10
revisions:
  - 2026-04-12
  - 2026-04-17
  - 2026-04-25
  - 2026-05-10
---

# Reverse An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Meta

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]], #arrays [[Arrays]]

## Pattern

Two Pointers (Opposite Ends)

---

## Difficulty

Easy  
#easy

---

## ⚡ Key Idea (Core Insight)

Swap elements from the start and end of the array, moving toward the center until the pointers meet or cross. This achieves an in-place reversal without extra space.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use `left` and `right` pointers; `swap(arr[left], arr[right])` and increment/decrement until `left >= right`.

---

## Approach

### Brute Force
- Create a new array, iterate the original array backwards, and copy elements into the new array.
- Time: O(N), Space: O(N)

### Optimal
- Use two pointers: `left = 0` and `right = n - 1`.
- Swap `arr[left]` and `arr[right]`.
- Increment `left`, decrement `right`.
- Stop when `left >= right`.
- Time: O(N), Space: O(1)

---

## Code (Python)

```python
class Solution:
    def reverseArray(self, arr: list[int]) -> None:
        """
        Reverses the input array in-place using two pointers.
        """
        left, right = 0, len(arr) - 1
        
        while left < right:
            # Swap elements at both ends
            arr[left], arr[right] = arr[right], arr[left]
            
            # Move pointers towards the middle
            left += 1
            right -= 1
```

---

## Dry Run (Smart Example)

**Input:** `arr = [1, -2, 3, 3, 5]`

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `left=0`, `right=4` | Swap `arr[0]` (1) and `arr[4]` (5). Array: `[5, -2, 3, 3, 1]` |
| 2 | `left=1`, `right=3` | Swap `arr[1]` (-2) and `arr[3]` (3). Array: `[5, 3, 3, -2, 1]` |
| 3 | `left=2`, `right=2` | `left` is not less than `right`. Loop terminates. |
| 4 | Final | Result: `[5, 3, 3, -2, 1]` |

---

## Edge Cases

- **Empty Array:** `[]` -> Loop never starts, returns empty.
- **Single Element:** `[1]` -> `left` and `right` start at 0, loop never starts.
- **Even Length:** `[1, 2, 3, 4]` -> Pointers cross perfectly.
- **Odd Length:** `[1, 2, 3]` -> Pointers meet at the middle element (no swap needed).

---

## Mistakes

- Using `left <= right` which performs an unnecessary swap of the middle element with itself.
- Forgetting to increment/decrement pointers, leading to an infinite loop.
- Returning a new array instead of modifying in-place (if requested).
- User Mistake: None.

---

## Complexity

Time: O(N) → We visit each element at most once (N/2 swaps).  
Space: O(1) → Reversal is performed in-place using only two pointer variables.

---

## Similar Problems

- [Reverse String](https://leetcode.com/problems/reverse-string/) - Easy
- [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) - Easy
- [Rotate Array](https://leetcode.com/problems/rotate-array/) - Medium
- [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy

---

## Tags and Properties

- #dsa #important #revisit  
- #arrays #twopointers #inplace  
- [[Two Pointers]] [[Arrays]]
- **Revision Date:** 2026-04-10
- **Problem Link:** [Reverse an Array - GeeksforGeeks](https://www.geeksforgeeks.org/problems/reverse-an-array/0)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-12)
- [ ] Day 7 Revision (2026-04-17)
- [ ] Day 15 Revision (2026-04-25)
- [ ] Day 30 Revision (2026-05-10)
