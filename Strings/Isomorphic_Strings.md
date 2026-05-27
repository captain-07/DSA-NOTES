---
created: 2026-04-28
revisions:
  - 2026-04-30
  - 2026-05-05
  - 2026-05-13
  - 2026-05-28
---

# Isomorphic Strings

---

## Metadata & Placement Tags

- **Target Companies:**
  - #LinkedIn #Google #Amazon #Microsoft #Adobe

- **Confidence Checklist:**
  - [ ] Low  
  - [ ] Medium  
  - [ ] High  

- **Concepts:**
  - #hashmap [[HashMap]], #string [[String]], #bijection [[One-to-One Mapping]]

---
## Pattern

HashMap (Bijection Mapping) / Frequency Transformation

---
## Difficulty

Easy
#easy

---

## ⚡ Key Idea (Core Insight)

The strings are isomorphic if there is a **one-to-one (bijective) mapping** between characters. This means:
1. Every character in `s` maps to exactly one character in `t`.
2. No two characters in `s` map to the same character in `t`.

---

## ⚡ Quick Recall (VERY IMPORTANT)

Use two HashMaps (or one Map + one Set) to ensure `s[i] -> t[i]` and `t[i] -> s[i]` are unique and consistent throughout the traversal.

---

## Approach

### Brute Force
- For every character in `s`, find all its indices and verify if the corresponding indices in `t` have the same character.
- Time: O(N²)
- Space: O(1)

### Optimal (Two HashMaps)
- Maintain two dictionaries: `map_st` (s to t) and `map_ts` (t to s).
- Iterate through both strings simultaneously.
- If a character is already mapped but points to a different character, return `False`.
- Otherwise, establish the mapping.
- Time: O(N)
- Space: O(K) where K is the alphabet size.

### Optimal (First Occurrence Index)
- Transform both strings into their first-occurrence index pattern.
- Example: "paper" -> `[0, 1, 0, 3, 4]`, "title" -> `[0, 1, 0, 3, 4]`.
- If patterns match, they are isomorphic.
- Time: O(N)
- Space: O(N)

---

## Code (Python)

```python
class Solution:
    def isIsomorphic(self, s: str, t: str) -> bool:
        # Dictionary to store mapping from s to t and t to s
        map_st, map_ts = {}, {}
        
        for char_s, char_t in zip(s, t):
            # Check if char_s is already mapped to something else
            if char_s in map_st and map_st[char_s] != char_t:
                return False
            
            # Check if char_t is already mapped from something else
            if char_t in map_ts and map_ts[char_t] != char_s:
                return False
            
            # Establish bidirectional mapping
            map_st[char_s] = char_t
            map_ts[char_t] = char_s
            
        return True
```

---

## Dry Run (Smart Example)

Input: `s = "paper"`, `t = "title"`

| Step | char_s | char_t | map_st | map_ts | Action |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 1 | p | t | {p: t} | {t: p} | New mapping |
| 2 | a | i | {p: t, a: i} | {t: p, i: a} | New mapping |
| 3 | p | t | {p: t, a: i} | {t: p, i: a} | Consistent with map |
| 4 | e | l | {p: t, ..., e: l} | {t: p, ..., l: e} | New mapping |
| 5 | r | e | {p: t, ..., r: e} | {t: p, ..., e: r} | New mapping |

**Result:** `True`

---

## Edge Cases

- **Different Lengths:** Usually same in constraints, but should return `False` immediately.
- **Empty Strings:** Technically isomorphic (`True`).
- **One-to-Many:** `s = "foo", t = "bar"` (`o` tries to map to `o` and `r`).
- **Many-to-One:** `s = "bar", t = "foo"` (`a` and `r` both try to map to `o`).

---

## Mistakes

- **Mapping only one way:** Forgetting to check if two different `s` characters map to the same `t` character.
- **Using a single Map:** Only checks `s -> t`, fails on `ab` -> `aa`.
- **User mistake:** No specific note provided. (Ensure you have a mental "Isomorphic == Bijection" trigger).

---

## Complexity

Time: O(N) → Single pass through the strings of length N.  
Space: O(1) or O(K) → The number of unique characters is capped by the character set (e.g., ASCII 128 or 256).

---

## Similar Problems

- [Word Pattern](https://leetcode.com/problems/word-pattern/) - Easy
- [Find and Replace Pattern](https://leetcode.com/problems/find-and-replace-pattern/) - Medium
- [Group Shifted Strings](https://leetcode.com/problems/group-shifted-strings/) - Medium

---

## Tags and Properties
- #dsa #important #revisit
- #string #hashmap [[HashMap]]
- **Revision Date:** 2026-04-28
- **Problem Link:** [LeetCode - Isomorphic Strings](https://leetcode.com/problems/isomorphic-strings/)

---
### 🔄 Revision Checklist
- [ ] Day 2 Revision (2026-04-30)
- [ ] Day 7 Revision (2026-05-05)
- [ ] Day 15 Revision (2026-05-13)
- [ ] Day 30 Revision (2026-05-28)
