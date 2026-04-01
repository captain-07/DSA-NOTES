---
created: 2026-04-01
revisions:
  - 2026-04-03
  - 2026-04-08
  - 2026-04-16
  - 2026-05-01
---

# Search In Rotated Sorted Array 2 [Duplicate Values]

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Google #Amazon #Microsoft #LinkedIn #Facebook

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #binarysearch [[Binary Search]]
  - #arrays [[Arrays]]
  - #twopointers [[Two Pointers]]

---
## Pattern

Modified Binary Search (Handling Duplicates)

---
## Difficulty

Medium  
#medium

---

## ⚡ Key Idea (Core Insight)

In a rotated sorted array **with duplicates**, the condition `nums[low] <= nums[mid]` no longer guarantees that the left half is sorted (e.g., `[1, 0, 1, 1, 1]`). When `nums[low] == nums[mid] == nums[high]`, we cannot determine which side is sorted, so we must shrink the search space by incrementing `low` and decrementing `high`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

If `nums[low] == nums[mid] == nums[high]`, just do `low += 1` and `high -= 1` to skip duplicates. Otherwise, proceed with standard Rotated Binary Search logic.

---

## Approach

### Brute Force
- Linear Search: Iterate through the array and check if any element equals the target.
- **Time Complexity:** O(N)

### Optimal
- **Modified Binary Search:**
  1. Initialize `low = 0`, `high = len(nums) - 1`.
  2. While `low <= high`:
     - Calculate `mid`.
     - If `nums[mid] == target`, return `True`.
     - **Handle Duplicates:** If `nums[low] == nums[mid] == nums[high]`, increment `low` and decrement `high`, then `continue`.
     - **Identify Sorted Half:** Check if left side `[low...mid]` or right side `[mid...high]` is sorted.
     - **Binary Search Logic:** If target lies within the sorted half, search there; otherwise, search the other half.

---

## Code (Python)

```python
def search(nums: list[int], target: int) -> bool:
    low, high = 0, len(nums) - 1
    
    while low <= high:
        mid = (low + high) // 2
        
        if nums[mid] == target:
            return True
            
        # The critical check for duplicates
        if nums[low] == nums[mid] == nums[high]:
            low += 1
            high -= 1
            continue
            
        # Check if Left half is sorted
        if nums[low] <= nums[mid]:
            # Target is in the sorted left half
            if nums[low] <= target < nums[mid]:
                high = mid - 1
            else:
                low = mid + 1
        # Right half must be sorted
        else:
            # Target is in the sorted right half
            if nums[mid] < target <= nums[high]:
                low = mid + 1
            else:
                high = mid - 1
                
    return False
```

---

## Dry Run (Smart Example)

**Input:** `nums = [1, 0, 1, 1, 1]`, `target = 0`

| Step | low | mid | high | nums[mid] | Explanation |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | 0 | 2 | 4 | 1 | `nums[0]==nums[2]==nums[4] (1==1==1)`. Shrink: `low=1, high=3`. |
| 2 | 1 | 2 | 3 | 1 | `nums[1]=0, nums[2]=1`. Left half `[0, 1]` is sorted. `0 <= 0 < 1` is True. `high = mid-1 = 1`. |
| 3 | 1 | 1 | 1 | 0 | `nums[1] == target`. Return **True**. |

---

## Edge Cases

- **All elements identical:** `[1, 1, 1]`, target `0` → Correctly returns `False` after shrinking.
- **Array size 1:** `[1]`, target `1` → Correctly returns `True`.
- **Target at pivot:** `[2, 5, 6, 0, 0, 1, 2]`, target `0` → Standard rotated logic handles this.
- **Empty Array:** Handled by `low <= high` condition.

---

## Mistakes

- **Forget duplicate check:** If you don't check `nums[low] == nums[mid] == nums[high]`, the code will fail on cases like `[1, 0, 1, 1, 1]`.
- **Misplacing the `continue`:** After shrinking `low` and `high`, you must skip the rest of the loop to re-evaluate `mid`.
- **Using `True/False` instead of index:** Read the problem carefully; this version (Part 2) usually asks for a boolean, while Part 1 asks for an index.

---

## Complexity

- **Time:** O(log N) on average; O(N) in the worst case (e.g., all elements are duplicates).
- **Space:** O(1) as no extra space is used.

---

## Tags and Properties

- #dsa #important #revisit #searching
- [[Binary Search]] [[Rotated Sorted Array]]
- Revision Date: 2026-04-01
- Related: [[Search In Rotated Sorted Array 1]]

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-03)
- [ ] Day 7 Revision (2026-04-08)
- [ ] Day 15 Revision (2026-04-16)
- [ ] Day 30 Revision (2026-05-01)
