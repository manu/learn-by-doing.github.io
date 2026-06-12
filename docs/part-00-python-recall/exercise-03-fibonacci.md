---
title: "0.3 Fibonacci Shelf Numbers"
parent: Python Recall Bootcamp
nav_order: 3
---

# Exercise 0.3 — Fibonacci Shelf Numbers

## The Story

The library is being redesigned. The architect has decided that each bookshelf will be numbered using the Fibonacci sequence — because the numbers grow in a way that mirrors how shelf capacity increases as you go deeper into the library.

The librarian wants a quick program: given how many shelves there are, print all the shelf numbers.

This exercise introduces *loops* — the idea that a computer can repeat something many times without you writing it out each time.

## What to Build

Your program should ask how many shelf numbers to generate and print the Fibonacci sequence up to that count.

```
How many shelves? 8
1, 1, 2, 3, 5, 8, 13, 21
```

The Fibonacci rule: each number is the sum of the two before it.
The sequence starts: 1, 1, 2, 3, 5, 8, 13, 21, 34, 55 ...

## Topics You Will Need

- `input()` and `int()` — to get the count
- Variables — you will need at least two variables that keep updating
- `while` loop — to keep generating numbers until you reach the count
- `print()` — to display results

## Before You Start — Think About This

1. To generate the next Fibonacci number, you need the previous two. How many variables do you need to track at minimum?
2. When you calculate the next number, you need to update your variables. What is the order of those updates? Does it matter?
3. Try working out the first 5 numbers by hand, on paper, tracking what your two variables would hold at each step. This is called *tracing* a program — it is how engineers debug before they run code.
4. How will your loop know when to stop?

## When You're Stuck

- Start by solving it for exactly 5 numbers, without a loop. Write out each step. Then see the pattern in what you are repeating.
- When updating two variables that depend on each other (`a` and `b`), order matters. If you update `a` first, you have lost the original value of `a` when you need it to update `b`. Think about how to handle this.
- A `while` loop runs as long as a condition is true. You need a counter that increases by 1 each time through the loop, and the loop stops when the counter reaches the total you want.

## Once It Works — Go Further

1. Instead of printing all numbers on one line separated by commas, print each number on its own line with its position: `Shelf 1: 1`, `Shelf 2: 1`, `Shelf 3: 2`, and so on.
2. Make the sequence start from 0 instead of 1 (the other common version: 0, 1, 1, 2, 3, 5 ...).
3. Given a shelf number (like `21`), check whether it *is* a Fibonacci number. How would you do that?
