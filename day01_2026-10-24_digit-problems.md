# Digit Problems in Python

The key idea used in all three problems:

- `num % 10` gives the **last digit**
- `num // 10` **removes** the last digit
- Loop `while num > 0` runs once per digit

---

## Problem 1: Extraction of Digits from an Integer

**Question:** Given an integer `n = 5873`, print each of its digits.

```python
n = 5873
num = n

while num > 0:
    last_digit = num % 10
    print(last_digit)
    num = num // 10
```

**Dry run:**

| num  | num % 10 (printed) | num // 10 |
|------|--------------------|-----------|
| 5873 | 3                  | 587       |
| 587  | 7                  | 58        |
| 58   | 8                  | 5         |
| 5    | 5                  | 0 → stop  |

**Output:**

```
3
7
8
5
```

> Digits come out in **reverse order** because we always pick the last digit first.

---

## Problem 2: Count the Number of Digits

**Question:** Given an integer `n = 5873`, find how many digits it has.

```python
n = 5873
count = 0
num = n

while num > 0:
    count += 1
    num = num // 10

print(count)
```

**Dry run:**

| num  | count | num // 10 |
|------|-------|-----------|
| 5873 | 1     | 587       |
| 587  | 2     | 58        |
| 58   | 3     | 5         |
| 5    | 4     | 0 → stop  |

**Output:**

```
4
```

> **Edge case:** If `n = 0`, the loop never runs and the count is `0`. Fix with `if n == 0: count = 1`.

---

## Problem 3: Palindrome Number

**Question:** Check whether a number reads the same forwards and backwards. For example, `121` is a palindrome and `5873` is not.

**Approach:** Reverse the number, then compare the reversed value with the original.

```python
n = 5873
num = n
last_digit = 0
res = 0

while num > 0:
    last_digit = num % 10
    res = res * 10 + last_digit
    num = num // 10

if res == n:
    print("Palindrome")
else:
    print("Not Palindrome")
```

**How `res = res * 10 + last_digit` works:** Multiplying by 10 shifts the existing digits one place left, then the new digit is added in the units place.

**Dry run for `n = 5873`:**

| num  | last_digit | res = res*10 + last_digit | num // 10 |
|------|------------|---------------------------|-----------|
| 5873 | 3          | 0*10 + 3 = **3**          | 587       |
| 587  | 7          | 3*10 + 7 = **37**         | 58        |
| 58   | 8          | 37*10 + 8 = **378**       | 5         |
| 5    | 5          | 378*10 + 5 = **3785**     | 0 → stop  |

`3785 != 5873` → **Output:** `Not Palindrome`

**Dry run for `n = 121`:**

| num | last_digit | res |
|-----|------------|-----|
| 121 | 1          | 1   |
| 12  | 2          | 12  |
| 1   | 1          | 121 |

`121 == 121` → **Output:** `Palindrome`

> **Note:** `res` must start at `0`, not `1`. Starting at `1` gives `1*10 + 3 = 13` in the first step, which makes the reversed number wrong.

