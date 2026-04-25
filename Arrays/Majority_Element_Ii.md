---
created: 2026-04-25
revisions:
  - 2026-04-27
  - 2026-05-02
  - 2026-05-10
  - 2026-05-25
---

# Majority Element-Ii

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Google #Microsoft #Meta #Adobe #Uber

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #arrays [[Arrays]] #voting [[Boyer-Moore Voting]] #hashmap [[HashMap]]

---
## Pattern

Extended Boyer-Moore Voting Algorithm  

---
## Difficulty

Medium  
#medium

---
## ⚡ Key Idea (Core Insight)

The problem asks for elements appearing **> n/3** times. Mathematically, there can be at most **two** such elements. We maintain two potential candidates and their respective counts. When we encounter a third distinct element, we "cancel" one count from both candidates.

---
## ⚡ Quick Recall (VERY IMPORTANT)

Two candidates, two counters. If the current element matches neither candidate and both counts > 0, decrement both. **Always verify counts with a second pass.**

---
## Approach

### Brute Force
- Use nested loops to count every element's frequency.
- Time: O(n²) | Space: O(1)

### Better
- Use a HashMap to store frequencies. Return keys with values > n/3.
- Time: O(n) | Space: O(n)

### Optimal
1. **Candidate Phase:** Initialize `cand1`, `cand2` and `count1`, `count2`.
2. Iterate through array:
   - If current equals `cand1`, increment `count1`.
   - Else if current equals `cand2`, increment `count2`.
   - Else if `count1 == 0`, set `cand1 = current`, `count1 = 1`.
   - Else if `count2 == 0`, set `cand2 = current`, `count2 = 1`.
   - Else, decrement both `count1` and `count2`.
3. **Verification Phase:** Reset counts and manually count occurrences of `cand1` and `cand2` to ensure they exceed n/3.

---
## Code (Python)

```python
class Solution:
    def majorityElement(self, nums: list[int]) -> list[int]:
        if not nums:
            return []
        
        # Phase 1: Finding potential candidates
        cand1, cand2 = None, None
        count1, count2 = 0, 0
        
        for n in nums:
            if n == cand1:
                count1 += 1
            elif n == cand2:
                count2 += 1
            elif count1 == 0:
                cand1, count1 = n, 1
            elif count2 == 0:
                cand2, count2 = n, 1
            else:
                count1 -= 1
                count2 -= 1
        
        # Phase 2: Verification
        result = []
        n_third = len(nums) // 3
        for cand in [cand1, cand2]:
            if cand is not None and nums.count(cand) > n_third:
                result.append(cand)
                
        return result
```

---
## Dry Run (Smart Example)

**Input:** `nums = [3, 2, 3, 1, 2, 2]` | **n/3 = 2**

| Step | Current | cand1 (count1) | cand2 (count2) | Explanation |
| :--- | :--- | :--- | :--- | :--- |
| 1 | 3 | 3 (1) | None (0) | Set cand1 |
| 2 | 2 | 3 (1) | 2 (1) | Set cand2 |
| 3 | 3 | 3 (2) | 2 (1) | Match cand1 |
| 4 | 1 | 3 (1) | 2 (0) | Decrement both (Triplet: 3,2,1) |
| 5 | 2 | 3 (1) | 2 (1) | Set cand2 (prev count was 0) |
| 6 | 2 | 3 (1) | 2 (2) | Match cand2 |

**Verification:** count(3)=2, count(2)=3. Only 2 > 2. **Result: [2]**

---
## Edge Cases

- **All elements same:** Both candidates might end up being the same or only one used.
- **No element > n/3:** Verification phase will return empty list.
- **Exactly two elements > n/3:** Handled by two-candidate logic.
- **Empty input:** Return empty list.
- **Array size < 3:** All unique elements are candidates.

---
## Mistakes

- **No specific note provided.** (Initial state).
- Forgetting the verification pass (essential because Boyer-Moore only finds potential candidates).
- Not using `elif` for the `count == 0` checks, leading to incorrect candidate overwrites.
- Not handling cases where `cand1` and `cand2` might initialize to the same value (e.g., using 0 as default when 0 is in `nums`).

---
## Complexity

- **Time:** O(n) → Two linear passes over the array.
- **Space:** O(1) → Constant space for two candidates and two counters.

---
## Similar Problems

- [Majority Element](https://leetcode.com/problems/majority-element/) - Easy
- [Check If a Number Is Majority Element in a Sorted Array](https://leetcode.com/problems/check-if-a-number-is-majority-element-in-a-sorted-array/) - Easy
- [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium

---
## Tags and Properties
- #dsa #important #revisit #boyermoore 
- [[Arrays]] [[Boyer-Moore Voting]]
- **Problem Link:** [Majority Element II - LeetCode](https://leetcode.com/problems/majority-element-ii/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-27)
- [ ] Day 7 Revision (2026-05-02)
- [ ] Day 15 Revision (2026-05-10)
- [ ] Day 30 Revision (2026-05-25)
