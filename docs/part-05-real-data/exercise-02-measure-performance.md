---
title: "5.2 Measure Performance"
parent: Real Data
nav_order: 2
---

# Exercise 5.2 — Measure Performance

## The Story

"It feels slow" is not a useful engineering observation. Engineers measure.

Before you can fix a performance problem, you need to know three things: how slow is it, which part is slow, and how does it change as data grows? Guessing is almost always wrong. The part you think is the bottleneck is often not the actual bottleneck.

This exercise teaches you to measure properly — so that when you apply a fix, you can prove the fix worked.

## What to Do

### Step 1 — Measure startup time

Add timing code to `storage.py` around the book loading:

```
(record the time just before load_books() runs)
(call load_books())
(record the time just after load_books() returns)
(print the difference)
```

Run with 10,000 books. Record the number.
Run with 50,000 books. Record the number.
Run with 100,000 books. Record the number.

### Step 2 — Measure search time

Add the same timing code around the search function. Run the same search query against:
- 10,000 books
- 50,000 books
- 100,000 books

Record each result.

### Step 3 — Build a results table

| Books | Startup time | Search time |
|-------|-------------|-------------|
| 10,000 | ? | ? |
| 50,000 | ? | ? |
| 100,000 | ? | ? |

### Step 4 — Find the pattern

Look at the numbers. When data doubles, does the time double? Does it more than double? Does it stay roughly the same?

Write one sentence explaining what you observe about how the program scales.

### Step 5 — Find the bottleneck

Which is slower — loading the data or searching it? By how much? Which problem is more important to fix first?

## What to Observe

The pattern of how time grows as data grows has a name in computer science: *time complexity*. A program that takes twice as long for twice the data is called linear — `O(n)`. A program that takes four times as long for twice the data is *quadratic* — `O(n²)`. Understanding which category your program falls into tells you how it will behave at scale.

You do not need to know the formal theory right now. But you should be able to observe the pattern in your own numbers.

## Topics You Will Need

- `import time` and `time.time()`
- Basic arithmetic to compute durations
- How to run the same experiment multiple times for consistent results
- The concept of a bottleneck — the slowest part of a pipeline determines the speed of the whole

## Before You Start — Think About This

1. If you measure search time once and get 0.3 seconds, is that a reliable measurement? What could cause it to vary between runs?
2. What is a *bottleneck*? If loading takes 5 seconds and search takes 0.01 seconds, which one matters more for the user experience? Which one is worth fixing first?
3. Your search function looks at every book in the list every time it runs. Is there a way to answer a search query without looking at every book? (You don't have to solve this yet — just think about whether it is possible.)

## When You're Stuck

- `time.time()` returns the current time in seconds as a float. Subtract the start time from the end time to get the duration.
- Run each measurement at least three times and use the average. The first run is often slower due to disk caching effects.
- If 100,000 books causes the program to crash with a `MemoryError`, that itself is important data — record it.

## Once It Works — Go Further

1. Look up what a *profiler* is. Python has a built-in one: run `python -m cProfile library.py` and read the output. Which function takes the most cumulative time? Does it match your intuition about where the bottleneck is?
2. Look up the term *algorithmic complexity* (or Big-O notation). After reading a short introduction, classify your search function: is it `O(n)`, `O(n²)`, or something else?
