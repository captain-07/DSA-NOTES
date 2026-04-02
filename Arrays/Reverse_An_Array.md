---
created: 2026-04-02
revisions:
  - 2026-04-04
  - 2026-04-09
  - 2026-04-17
  - 2026-05-02
---

# Reverse An Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Adobe #Apple #Meta

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #twopointers [[Two Pointers]]
  - #arrays [[Arrays]]

## Pattern

Two Pointers (Opposite Ends)

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

The first and last elements swap positions, the second and second-to-last swap, and so on. By maintaining two pointers at the boundaries and moving them toward the center, we reverse the array in-place.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Swap `arr[left]` with `arr[right]` while `left < right`.

---

## Approach

### Brute Force
- Create a new array of the same size. Iterate through the original array from end to start and copy elements into the new array.
- **Complexity:** Time: O(N), Space: O(N)

### Better
- Use a Stack: Push all elements onto a stack, then pop them back into the array.
- **Complexity:** Time: O(N), Space: O(N)

### Optimal
- **Two Pointers (In-place):**
  1. Initialize `left = 0` and `right = len(arr) - 1`.
  2. While `left < right`:
     - Swap `arr[left]` and `arr[right]`.
     - Increment `left`.
     - Decrement `right`.
- **Complexity:** Time: O(N), Space: O(1)

---

## Code (Python)

```python
def reverse_array(arr):
    # Initialize pointers at both ends
    left = 0
    right = len(arr) - 1
    
    while left < right:
        # Swap elements at the pointers
        arr[left], arr[right] = arr[right], arr[left]
        
        # Move pointers towards the middle
        left += 1
        right -= 1
        
    return arr
```

---

## Dry Run (Smart Example)

**Input:** `arr = [10, -1, 5, 10, 2]`

| Step | Variables | Explanation | Array State |
| :--- | :--- | :--- | :--- |
| 1 | `left=0, right=4` | Swap `arr[0]`(10) and `arr[4]`(2) | `[2, -1, 5, 10, 10]` |
| 2 | `left=1, right=3` | Swap `arr[1]`(-1) and `arr[3]`(10) | `[2, 10, 5, -1, 10]` |
| 3 | `left=2, right=2` | `left < right` is False. Loop terminates. | `[2, 10, 5, -1, 10]` |

---

## Edge Cases

- **Empty Array:** `[]` -> Function handles it (loop doesn't run).
- **Single Element:** `[1]` -> `left` is not `< right`, stays same.
- **Even Length:** `[1, 2, 3, 4]` -> All pairs swap perfectly.
- **Odd Length:** `[1, 2, 3]` -> Middle element remains untouched.
- **Duplicates/Negatives:** Handled naturally by the swap logic.

---

## Mistakes

- **Recursive Approach:** Avoid for simple array reversal. It introduces O(N) space complexity due to the recursion stack, which is less efficient than the O(1) iterative approach.
- **Off-by-one errors:** Setting `right = len(arr)` instead of `len(arr) - 1`.
- **Loop Condition:** Using `left <= right` (unnecessary swap of the middle element in odd-length arrays).
- **Returning new list:** Forgetting to modify the array in-place when space is a constraint.

---

## Complexity

- **Time:** O(N) → Each element is visited at most once as pointers meet in the middle.
- **Space:** O(1) → Swapping is performed in-place without auxiliary data structures.

---

## Tags and Properties

- #dsa #important #revisit #basics
- #arrays [[Arrays]]
- #twopointers [[Two Pointers]]
- **Revision Date:** 2026-04-02
- **Related:** [[Reverse String]], [[Palindrome Linked List]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-04)
- [ ] Day 7 Revision (2026-04-09)
- [ ] Day 15 Revision (2026-04-17)
- [ ] Day 30 Revision (2026-05-02)
