---
created: 2026-04-02
revisions:
  - 2026-04-04
  - 2026-04-09
  - 2026-04-17
  - 2026-05-02
---

# Check If String Is Palindrome Or Not

---

## Metadata & Placement Tags

- **Target Companies:**
  - #Amazon #Microsoft #Google #Meta #Adobe #Apple

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #strings [[Strings]]
  - #twopointers [[Two Pointers]]

## Pattern

Two Pointers

---
## Difficulty

Easy #easy

---

## ⚡ Key Idea (Core Insight)

A palindrome reads the same forward and backward. Instead of reversing the whole string, use two pointers starting at opposite ends and move them toward the center, comparing characters at each step.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Initialize `left = 0` and `right = len(s) - 1`. While `left < right`, if `s[left] != s[right]`, it's not a palindrome.

---

## Approach

### Brute Force
- Create a reversed version of the string using slicing `s[::-1]` and compare it to the original.
- **Time Complexity:** O(N)
- **Space Complexity:** O(N) (due to the new reversed string)

### Better
- Use a Deque (Double-Ended Queue). Pop from both ends and compare.
- **Time Complexity:** O(N)
- **Space Complexity:** O(N)

### Optimal
- **Two Pointers:** 
  1. Set `left` pointer to 0 and `right` pointer to `n-1`.
  2. In a loop, check if `s[left] == s[right]`.
  3. If they match, increment `left` and decrement `right`.
  4. If they don't match, return `False`.
  5. If pointers meet or cross, return `True`.

---

## Code (Python)

```python
def is_palindrome(s: str) -> bool:
    # Optional: Pre-process to handle case and non-alphanumeric
    # s = "".join(char.lower() for char in s if char.isalnum())
    
    left = 0
    right = len(s) - 1
    
    while left < right:
        # Compare characters
        if s[left] != s[right]:
            return False
        
        # Move pointers inward
        left += 1
        right -= 1
        
    return True
```

---

## Dry Run (Smart Example)

Input: `s = "RaceCar"` (Processed to `"racecar"`)

| Step | Variables | Explanation |
| :--- | :--- | :--- |
| 1 | `left=0 ('r')`, `right=6 ('r')` | Characters match. Move pointers. |
| 2 | `left=1 ('a')`, `right=5 ('a')` | Characters match. Move pointers. |
| 3 | `left=2 ('c')`, `right=4 ('c')` | Characters match. Move pointers. |
| 4 | `left=3 ('e')`, `right=3 ('e')` | `left` is no longer `< right`. Loop ends. |
| 5 | **Result** | Return `True`. |

---

## Edge Cases

- **Empty String:** Usually considered a palindrome.
- **Single Character:** Always a palindrome.
- **Case Sensitivity:** "Abba" is not a palindrome unless converted to lowercase.
- **Spaces/Punctuation:** "race car" vs "racecar" (depends on problem constraints).

---

## Mistakes

- **Recursive approach:** Avoid this in interviews for simple string checks. It incurs $O(N)$ space complexity due to the recursion stack, whereas two pointers use $O(1)$.
- **Forgetting to handle case:** Comparing 'A' and 'a' will return `False`.
- **Inefficient Cleaning:** Using repeated string concatenation inside a loop to remove spaces (O(N²) complexity). Use `.join()` or pointers.

---

## Complexity

Time: O(N) → We traverse the string at most once.  
Space: O(1) → Only two integer pointers are used, regardless of input size.

---

## Tags and Properties
  - #dsa #important #revisit  
  - #palindrome #string-manipulation #easy-interview
  - [[Two Pointers]] [[Strings]]
  - Revision Date: 2026-04-02

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-04)
- [ ] Day 7 Revision (2026-04-09)
- [ ] Day 15 Revision (2026-04-17)
- [ ] Day 30 Revision (2026-05-02)
