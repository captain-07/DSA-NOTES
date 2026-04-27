---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Second Largest Element

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Adobe #Samsung #MorganStanley

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]], #iteration [[Iteration]], #greedy [[Greedy]]

## Pattern

Single Pass Traversal (Two-Variable Tracking)

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

Maintain two variables: `largest` and `second_largest`. As you traverse, if an element is greater than `largest`, the old `largest` becomes the new `second_largest`. If it's smaller than `largest` but greater than `second_largest`, update only `second_largest`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Update `second_largest` in two cases: when a new "king" (`largest`) is found, or when a new "runner-up" (better than current `second_largest`) is found.

---

## Approach

### Brute Force
- Sort the array in descending order and return the second element. Handle duplicates by skipping elements equal to the first.
- **Time:** O(N log N)

### Better
- Two-pass approach: 1st pass to find the maximum element, 2nd pass to find the largest element that is strictly less than the maximum.
- **Time:** O(N) (but 2 traversals)

### Optimal
- **Single Pass:** Initialize `largest = second_largest = -1` (or -infinity).
- Traverse the array once.
- If `arr[i] > largest`: update `second_largest = largest` and `largest = arr[i]`.
- Else if `arr[i] > second_largest` AND `arr[i] != largest`: update `second_largest = arr[i]`.

---

## Code (Python)

```python
class Solution:
    def getSecondLargest(self, arr):
        # Initialize variables with -1 (assuming positive integers)
        # or float('-inf') for general cases
        largest = -1
        second_largest = -1
        
        for x in arr:
            if x > largest:
                # Old largest becomes second largest
                second_largest = largest
                largest = x
            elif x > second_largest and x != largest:
                # Update second largest if x is better than current runner-up
                second_largest = x
                
        return second_largest
```

---

## Dry Run (Smart Example)

**Input:** `arr = [12, 35, 1, 10, 34, 1]`

| Step | Current `x` | `largest` | `second_largest` | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 12 | 12 | -1 | `12 > -1`, `largest` updated. |
| 2 | 35 | 35 | 12 | `35 > 12`, `second` gets 12, `large` gets 35. |
| 3 | 1 | 35 | 12 | `1 < 12`, no change. |
| 4 | 10 | 35 | 12 | `10 < 12`, no change. |
| 5 | 34 | 35 | 34 | `34 > 12` and `34 < 35`, `second` updated. |
| 6 | 1 | 35 | 34 | No change. |

---

## Edge Cases

- **Array size < 2:** Return -1.
- **All elements same:** `[10, 10, 10]` → Return -1 (no second largest).
- **Descending order:** `[30, 20, 10]` → Correctly shifts values.
- **Negative numbers:** Use `float('-inf')` for initialization instead of `-1`.

---

## Mistakes

- **Initialization Error:** Initializing `second_largest` with 0 when the array contains negative numbers.
- **Duplicate Ignorance:** Failing to check `x != largest`, which results in `second_largest` becoming equal to `largest`.
- **User Mistake:** No specific note provided.

---

## Complexity

Time: O(N) → Single traversal of the input array.  
Space: O(1) → Only two variables used regardless of input size.

---

## Similar Problems

- [Largest Element in Array](https://www.geeksforgeeks.org/problems/largest-element-in-array1558/1) - Easy
- [Third Largest Element](https://leetcode.com/problems/third-maximum-number/) - Easy
- [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium

---

## Tags and Properties
- #dsa #important #revisit  
- #arrays #top-interview-questions
- [[Arrays]] [[Iteration]]
- **Revision Date:** 2026-04-25
- **Problem Link:** [GeeksforGeeks - Second Largest](https://www.geeksforgeeks.org/problems/second-largest3735/1)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
