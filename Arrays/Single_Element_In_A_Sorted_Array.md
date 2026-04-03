---
created: 2026-04-03
revisions:
  - 2026-04-05
  - 2026-04-10
  - 2026-04-18
  - 2026-05-03
---

# Single Element In A Sorted Array

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Facebook #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #bitmanipulation [[Bit Manipulation]]
  - #array [[Array]]

---
## Pattern

Binary Search on Index Parity (Even-Odd logic)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

The array is divided into two halves by the single element.  
1. **Left Half:** Pairs follow the `(even index, odd index)` pattern. The first instance is at `even`, the second at `odd`.  
2. **Right Half:** After the single element, the pattern shifts to `(odd index, even index)`.  
By checking the index of the current pair, we determine if we are before or after the single element.

---

## ⚡ Quick Recall (VERY IMPORTANT)

- **Left of Single:** `nums[mid] == nums[mid ^ 1]` where `mid` is the first element of a potential pair.
- **Goal:** Find the first index where the `(even, odd)` parity breaks.

---

## Approach

### Brute Force
- Linear search through the array. Check if `nums[i]` is different from its neighbors.
- **Time:** $O(N)$
- **Space:** $O(1)$

### Better
- XOR all elements. Since $x \oplus x = 0$, the remaining value is the single element.
- **Time:** $O(N)$
- **Space:** $O(1)$

### Optimal
1. Use Binary Search with `low = 0`, `high = n - 2`.
2. Calculate `mid`.
3. Check if `mid` is in the "Left Half":
   - If `mid` is even, the next element should be the same (`nums[mid] == nums[mid+1]`).
   - If `mid` is odd, the previous element should be the same (`nums[mid] == nums[mid-1]`).
   - **Shortcut:** `if nums[mid] == nums[mid ^ 1]`, we are in the left half.
4. If in Left Half: `low = mid + 1` (Move right).
5. Else: `high = mid - 1` (Move left).
6. Result is `nums[low]`.

---

## Code (Python)

```python
def singleNonDuplicate(nums: list[int]) -> int:
    low = 0
    high = len(nums) - 2  # Guard against index out of bounds
    
    while low <= high:
        mid = (low + high) // 2
        
        # Check if mid is the first element of a pair (even index) 
        # or second element (odd index) and if it matches its partner.
        # mid ^ 1: if mid is even, returns mid + 1; if odd, returns mid - 1.
        if nums[mid] == nums[mid ^ 1]:
            # Pattern is intact: Single element is to the right
            low = mid + 1
        else:
            # Pattern is broken: Single element is at or to the left
            high = mid - 1
            
    return nums[low]
```

---

## Dry Run (Smart Example)

Input: `nums = [1, 1, 2, 3, 3, 4, 4]`

| Step | low | high | mid | `nums[mid]` | `nums[mid ^ 1]` | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 5 | 2 | 2 | `nums[3]` (3) | `2 != 3`. Pattern broken. Move `high = 1`. |
| 2 | 0 | 1 | 0 | 1 | `nums[1]` (1) | `1 == 1`. Pattern intact. Move `low = 1`. |
| 3 | 1 | 1 | 1 | 1 | `nums[0]` (1) | `1 == 1`. Pattern intact. Move `low = 2`. |
| 4 | 2 | 1 | - | - | - | `low > high`. Loop ends. Return `nums[2] = 2`. |

---

## Edge Cases

- **Single Element at Start:** `[1, 2, 2, 3, 3]` -> Binary search correctly shifts `high` left.
- **Single Element at End:** `[1, 1, 2, 2, 3]` -> Binary search shifts `low` right until the end.
- **Array of Size 1:** `[1]` -> Handled by loop conditions or early return.
- **Two Elements:** Not possible per problem constraints (always odd length).

---

## Mistakes

- **Index Out of Bounds:** Using `high = len(nums) - 1` can lead to issues with `mid ^ 1`. Use `n - 2`.
- **User Mistake (Half Elimination):** We eliminate the left half if `nums[mid] == nums[mid ^ 1]` because that condition *only* holds true when every pair before `mid` is correctly aligned as `(even, odd)`. If the condition fails, the "disruption" (the single element) must have occurred at or before `mid`.
- **Even/Odd Confusion:** Forgetting that the *first* element of a normal pair must be at an *even* index.

---

## Complexity

- **Time:** $O(\log N)$ → Binary search reduces search space by half each step.
- **Space:** $O(1)$ → Only a few variables used.

---

## Tags and Properties
- #dsa #important #revisit #interview-favorite
- [[Binary Search]] [[Bit Manipulation]]
- Revision Date: 2026-04-03
- Related: [[Find Duplicate Number]], [[Search in Rotated Sorted Array]]

---

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-05)
- [ ] Day 7 Revision (2026-04-10)
- [ ] Day 15 Revision (2026-04-18)
- [ ] Day 30 Revision (2026-05-03)
