# Day 04 - 2026-10-28

**Topic:** Recursion basics (printing, sums, factorial, reversing an array, palindrome)

---

## Problem 1: Print a Name N Times

**Question:** Given a name and an integer `n`, print the name `n` times using recursion.

```
Input:
Mohan
3

Output:
Mohan
Mohan
Mohan
```

### Solution

```python
def printName(name, count, n):
    if count == n:
        return
    print(name)
    printName(name, count + 1, n)


name = input()
n = int(input())
printName(name, 0, n)
```

---

## Problem 2: Print a Number N Times

**Question:** Given two integers `x` and `n`, print `x` exactly `n` times using recursion.

```
Input:
15 4

Output:
15
15
15
15
```

### Solution

```python
def printX(x, n):
    if n <= 0:
        return
    print(x)
    printX(x, n - 1)


x, n = map(int, input().split())
printX(x, n)
```

---

## Problem 3: Print 1 to N

**Question:** Given an integer `n`, print all numbers from `1` to `n` in increasing order using recursion.

```
Input:
4

Output:
1
2
3
4
```

### Solution

```python
def printOneToN(i, n):
    if i > n:
        return
    print(i)
    printOneToN(i + 1, n)


n = int(input())
printOneToN(1, n)
```

---

## Problem 4: Sum of First N Numbers (Running Total as a Parameter)

**Question:** Given `n`, find `1 + 2 + ... + n`. Pass the running total to each recursive call and print it when the recursion ends.

```
Input:
10

Output:
55
```

### Solution

```python
def sumParam(total, i, n):
    if i > n:
        print(total)
        return
    sumParam(total + i, i + 1, n)


n = int(input())
sumParam(0, 1, n)
```

---

## Problem 5: Sum of First N Numbers (Returning the Result)

**Question:** Given `n`, find `1 + 2 + ... + n`. Each call returns `n` plus the sum of the smaller problem.

```
Input:
10

Output:
55
```

### Solution

```python
def sumN(n):
    if n <= 0:
        return 0
    return n + sumN(n - 1)


n = int(input())
print(sumN(n))
```

---

## Problem 6: Factorial of N

**Question:** Given a non-negative integer `n`, find `n! = n * (n-1) * ... * 1`, where `0! = 1`.

```
Input:
5

Output:
120
```

### Solution

```python
def factorial(n):
    if n <= 1:
        return 1
    return n * factorial(n - 1)


n = int(input())
print(factorial(n))
```

---

## Problem 7: Reverse an Array

**Question:** Given an array of integers, reverse it in place using recursion. Swap the outer pair, then recurse on the inner part.

```
Input:
1 2 3 4 5 6 7 8

Output:
8 7 6 5 4 3 2 1
```

### Solution

```python
def reverse(nums, left, right):
    if left >= right:
        return
    nums[left], nums[right] = nums[right], nums[left]
    reverse(nums, left + 1, right - 1)


nums = list(map(int, input().split()))
reverse(nums, 0, len(nums) - 1)
print(*nums)
```

---

## Problem 8: Check Palindrome String

**Question:** Given a string `s`, check whether it reads the same forwards and backwards using recursion. Compare the outer pair of characters, then recurse inward.

```
Input:
madam

Output:
True
```

### Solution

```python
def checkPalindrome(s, left, right):
    if left >= right:
        return True
    if s[left] != s[right]:
        return False
    return checkPalindrome(s, left + 1, right - 1)


s = input()
print(checkPalindrome(s, 0, len(s) - 1))
```

---

## Key Takeaways

1. Every recursive function needs a **base case** to stop, or it ends in a `RecursionError`.
2. **Parameterized recursion** carries the result in the arguments (Problem 4).
3. **Functional recursion** returns the result from each call (Problems 5 and 6).
4. **Two-pointer recursion** (`left`, `right`) works well for reversing and palindrome checks (Problems 7 and 8).
5. Use `global` only when a function must change a variable defined outside it; passing values as parameters is cleaner.
