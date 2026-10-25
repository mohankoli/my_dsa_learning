# Day 02 - 2026-10-25

**Topics:** Two pointers, Frequency map (dictionary)

---

## Problem 1: Reverse String

**Question:** Reverse a list of characters **in place** (modify the original list, do not create a new one).

```
Input:  s = ["h","e","l","l","o"]
Output: ["o","l","l","e","h"]
```

**Approach (two pointers):** Start one pointer at each end, swap the two characters, then move both pointers toward the middle. Stop when they meet.

```python
s = ["h","e","l","l","o"]
left = 0
right = len(s) - 1

while left < right:
    s[left], s[right] = s[right], s[left]
    left += 1
    right -= 1

print(s)
```

**Dry run:**

| left | right | swap   | s after swap            |
|------|-------|--------|-------------------------|
| 0    | 4     | h ↔ o  | ["o","e","l","l","h"]   |
| 1    | 3     | e ↔ l  | ["o","l","l","e","h"]   |
| 2    | 2     | stop (left < right is false) |   |

**Output:**

```
['o', 'l', 'l', 'e', 'h']
```

> **Why `left < right`:** In an odd-length list the middle character stays in place, so it never needs a swap.

**Complexity:** Time O(n), Space O(1)

---

## Problem 2: Store Frequency in Dictionary (Method 1 - `if/else`)

**Question:** Given a list of integers `nums`, store the frequency of every element in a dictionary. Then print the frequency of a given number `x`.

```
Input:  nums = [5, 6, 7, 7, 1, 9, 111, 1, 1, 5, 1, 1]
        x = 1
Output: 5
```

**Approach:** Loop through the list. If the number is already in the dictionary, add 1 to its count. Otherwise, add it with count 1.

```python
nums = [5, 6, 7, 7, 1, 9, 111, 1, 1, 5, 1, 1]
x = 1
freq_map = {}

for i in range(0, len(nums)):
    if nums[i] in freq_map:
        freq_map[nums[i]] += 1
    else:
        freq_map[nums[i]] = 1

print(freq_map)
print(freq_map[x])
```

**Dry run (first few steps):**

| i | nums[i] | already in map? | freq_map after step              |
|---|---------|-----------------|----------------------------------|
| 0 | 5       | No              | {5: 1}                           |
| 1 | 6       | No              | {5: 1, 6: 1}                     |
| 2 | 7       | No              | {5: 1, 6: 1, 7: 1}               |
| 3 | 7       | Yes             | {5: 1, 6: 1, 7: 2}               |
| 4 | 1       | No              | {5: 1, 6: 1, 7: 2, 1: 1}         |
| … | …       | …               | …                                |

**Output:**

```
{5: 2, 6: 1, 7: 2, 1: 5, 9: 1, 111: 1}
5
```

**Complexity:** Time O(n), Space O(n)

---

## Problem 3: Store Frequency in Dictionary (Method 2 - `.get()`)

**Question:** Solve the same frequency problem without using `if/else`.

```
Input:  nums = [5, 6, 7, 7, 1, 9, 111, 1, 1, 5, 1, 1]
        x = 1
Output: 5
```

**Approach:** `dict.get(key, 0)` returns the current count of `key`, or `0` if the key is not in the dictionary yet. Add 1 to that and store it back.

```python
nums = [5, 6, 7, 7, 1, 9, 111, 1, 1, 5, 1, 1]
x = 1
hash_map = {}

for i in range(0, len(nums)):
    hash_map[nums[i]] = hash_map.get(nums[i], 0) + 1

print(hash_map)
print(hash_map[x])
```

**Output:**

```
{5: 2, 6: 1, 7: 2, 1: 5, 9: 1, 111: 1}
5
```

> **Tip:** `hash_map[x]` raises a `KeyError` if `x` is not in the list. Use `hash_map.get(x, 0)` to safely print `0` instead.

**Complexity:** Time O(n), Space O(n)

---

## Common Errors I Made Today

| Wrong code               | Correct code              | Error       |
|--------------------------|---------------------------|-------------|
| `for i in nums(0, len(nums))` | `for i in range(0, len(nums))` | `TypeError: 'list' object is not callable` |
| `if num[i] in freq_map`  | `if nums[i] in freq_map`  | `NameError: name 'num' is not defined` |
| `""""` (4 quotes)        | `"""` (3 quotes)          | Works by accident, but adds an extra `"` inside the string |
