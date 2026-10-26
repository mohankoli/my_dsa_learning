# Day 03 - 2026-10-26

**Topic:** Hashing basics (number hashing, character hashing)

---

## Problem 1: Number Hashing (Count Frequencies)

**Question:** You are given two integer arrays `n` and `m`. For each element in `m`, find how many times it appears in `n`.

```
Input:
n = [5, 3, 2, 2, 1, 5, 5, 7, 5, 10]
m = [10, 111, 1, 9, 5, 67, 2]

Output:
10  -> 1
111 -> 0
1   -> 1
9   -> 0
5   -> 4
67  -> 0
2   -> 2
```

**Constraints:**

1. `1 <= n[i] <= 10`
2. `n` can have up to 10^8 elements
3. `m` can have up to 10^8 elements

**Why not a nested loop?** Checking every element of `m` against every element of `n` is O(n × m), which is far too slow for 10^8 elements. Hashing does it in O(n + m).

### Solution (dictionary)

```python
n = [5, 3, 2, 2, 1, 5, 5, 7, 5, 10]
m = [10, 111, 1, 9, 5, 67, 2]
hash_map = {}

for i in range(0, len(n)):
    hash_map[n[i]] = hash_map.get(n[i], 0) + 1

print(hash_map)

for i in m:
    if i in hash_map:
        print(i, "->", hash_map[i])
    else:
        print(i, "->", 0)
```

**Output:**

```
{5: 4, 3: 1, 2: 2, 1: 1, 7: 1, 10: 1}
10 -> 1
111 -> 0
1 -> 1
9 -> 0
5 -> 4
67 -> 0
2 -> 2
```

**Shorter second loop:**

```python
for i in m:
    print(i, "->", hash_map.get(i, 0))
```

**Complexity:** Time O(n + m), Space O(n)

### Mistakes I made

| Wrong code | Problem | Fix |
|------------|---------|-----|
| `if i == hash_map[i]` | Compares the number with its count | `if i in hash_map` |
| `if ...` / `else` without `:` | `SyntaxError` | Add `:` at the end |
| `hash_map[111]` | `KeyError` (111 not in map) | Check `in` first, or use `.get(i, 0)` |

---

## Problem 2: Character Hashing

**Question:** You are given a string `s` and a list of query characters `q`. For each character in `q`, find how many times it appears in `s`.

```
Input:
s = "azyxyyzaaaa"
q = ["a", "a", "y", "x"]

Output:
a -> 5
a -> 5
y -> 3
x -> 1
```

**Constraints:**

1. `'a' <= s[i] <= 'z'` (only lowercase letters)

**Key idea:** Convert each letter to an index from 0 to 25 using `ord(ch) - ord('a')`, which is the same as `ord(ch) - 97`.

| ch | ord(ch) | ord(ch) - 97 |
|----|---------|--------------|
| a  | 97      | 0            |
| x  | 120     | 23           |
| y  | 121     | 24           |
| z  | 122     | 25           |

To convert an index back to a letter: `chr(idx + 97)`

### Method 1: Hash array of size 26

```python
s = "azyxyyzaaaa"
q = ["a", "a", "y", "x"]

hash_arr = [0] * 26

for ch in s:
    hash_arr[ord(ch) - 97] += 1

for ch in q:
    print(ch, "->", hash_arr[ord(ch) - 97])
```

**Hash array after counting:** index 0 (`a`) = 5, index 23 (`x`) = 1, index 24 (`y`) = 3, index 25 (`z`) = 2. All other indexes are 0.

### Method 2: Dictionary with `-97` keys

```python
s = "azyxyyzaaaa"
q = ["a", "a", "y", "x"]

hash_map = {}

for ch in s:
    idx = ord(ch) - 97
    hash_map[idx] = hash_map.get(idx, 0) + 1

print(hash_map)

for ch in q:
    idx = ord(ch) - 97
    print(ch, "->", hash_map.get(idx, 0))
```

**Output:**

```
{0: 5, 25: 2, 24: 3, 23: 1}
a -> 5
a -> 5
y -> 3
x -> 1
```

**Dry run (first 4 characters):**

| ch | ord(ch) | idx = ord(ch) - 97 | hash_map after step |
|----|---------|--------------------|---------------------|
| a  | 97      | 0                  | {0: 1}              |
| z  | 122     | 25                 | {0: 1, 25: 1}       |
| y  | 121     | 24                 | {0: 1, 25: 1, 24: 1} |
| x  | 120     | 23                 | {0: 1, 25: 1, 24: 1, 23: 1} |

### Method 3: Dictionary with characters as keys

```python
s = "azyxyyzaaaa"
q = ["a", "a", "y", "x"]

hash_map = {}

for ch in s:
    hash_map[ch] = hash_map.get(ch, 0) + 1

print(hash_map)

for ch in q:
    print(ch, "->", hash_map.get(ch, 0))
```

**Output:**

```
{'a': 5, 'z': 2, 'y': 3, 'x': 1}
a -> 5
a -> 5
y -> 3
x -> 1
```

### Complexity

| Method | Time | Space |
|--------|------|-------|
| Array of size 26 | O(len(s) + len(q)) | O(26), constant |
| Dict with `-97` keys | O(len(s) + len(q)) | O(distinct characters) |
| Dict with char keys | O(len(s) + len(q)) | O(distinct characters) |

> **Note:** The `-97` trick is required for a list, because list indexes must be 0 to 25. A dictionary can use the character itself as the key, so `-97` is optional there.

> **Bonus:** If `s` can contain any character (uppercase, digits, symbols), use a list of size 256 with `hash_arr[ord(ch)]`, or simply use a dictionary.

---

## Related LeetCode Practice

| # | Problem | Level |
|---|---------|-------|
| 1512 | Number of Good Pairs | Easy |
| 1207 | Unique Number of Occurrences | Easy |
| 387 | First Unique Character in a String | Easy |
| 2956 | Find Common Elements Between Two Arrays | Easy |
| 349 | Intersection of Two Arrays | Easy |
| 350 | Intersection of Two Arrays II | Easy |
| 1 | Two Sum | Easy |
