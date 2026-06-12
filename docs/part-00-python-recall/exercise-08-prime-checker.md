---
title: "0.8 Prime Checker"
parent: Python Recall Bootcamp
nav_order: 8
---

# Exercise 0.8 — Prime Checker

## The Story

The library assigns special IDs to its rarest, most valuable books — first editions, signed copies, and antique texts. The ID assigned to each rare book is always a prime number. When a new rare book arrives, the librarian needs to pick the next available prime number ID.

Your program will check whether a given number is prime. This is also your first introduction to thinking about *efficiency* — there is a naive way to solve this and a smarter way, and the difference matters when the numbers get large.

## What to Build

Your program should keep asking for numbers until the user types `0` to quit.

```
Enter a number (0 to quit): 17
17 is prime.

Enter a number (0 to quit): 100
100 is not prime.

Enter a number (0 to quit): 97
97 is prime.

Enter a number (0 to quit): 1
1 is not prime.

Enter a number (0 to quit): 0
Done.
```

Note: 1 is *not* considered a prime number. Your program must handle this case.

## Topics You Will Need

- `input()` and `int()` — to get each number
- `while` loop — to keep the program running
- `for` loop with `range()` — to check divisibility
- Modulo operator `%` — if `n % d == 0`, then `d` divides `n` evenly
- `break` — to stop a loop early when you have found what you need
- Boolean variable or `flag` — to track whether a divisor was found

## Before You Start — Think About This

1. A prime number is only divisible by 1 and itself. So to check if `n` is prime, you need to test whether any number between 2 and `n-1` divides it evenly. How do you check "divides evenly" in Python?
2. If you are checking 9,973 (a large prime), you would test every number from 2 to 9,972 — that is almost 10,000 checks. But think: if no number up to the *square root* of 9,973 divides it, can any number larger than the square root divide it? Why or why not? (This is the key insight for the efficient version.)
3. What should your program do when it finds a divisor — should it keep checking all the remaining numbers, or can it stop?
4. How does your program track whether a divisor was found or not? Think about what information you need *after* the loop finishes.

## When You're Stuck

- To check all numbers from 2 to `n-1`: use `for d in range(2, n):` — here `d` stands for "divisor".
- The modulo operator: `17 % 5` gives `2` (the remainder). If the remainder is `0`, the number divides exactly.
- To stop the loop the moment you find a divisor, use `break`. Then after the loop, check if you broke out early or completed all checks.
- For the efficient version: `import math` and use `int(math.sqrt(n))` — only check up to and including the square root.

## Once It Works — Go Further

1. Instead of checking one number at a time, print all prime numbers between 1 and 200. This is called the *Sieve of Eratosthenes* — look it up.
2. Given a number, find the next prime number after it. The librarian needs this to assign the next available rare-book ID.
3. Count how many prime numbers exist below 1,000. Then below 10,000. Does the density of primes increase or decrease as numbers get larger?
