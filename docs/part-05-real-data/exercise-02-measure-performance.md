---
title: "5.2 Measure Performance"
parent: Real Data
nav_order: 2
---

# Exercise 5.2 — Measure Performance

## The Story

The librarian asks: "How slow is it?"

"It feels slow," you say.

"How slow is slow? Is it 2 seconds slow or 20 seconds slow? Does it get worse as we add more books, or does it stay the same? Which part is slow — the startup, or the search?"

You cannot answer any of these questions. You only know it *feels* slow.

This is the difference between a complaint and a measurement. In engineering, "it feels slow" is the beginning of an investigation, not the end. Before you can fix a performance problem, you need to know:

1. How slow is it, in numbers?
2. Which part is the bottleneck?
3. How does the slowness grow as data grows?

Only measurements answer these questions. Guessing is almost always wrong — engineers consistently underestimate how much the *wrong* part matters and how little the *right* part does.

## What to Do

### Part A — Add timing to the library

Add code to measure exactly how long each major operation takes. Measure at least two points:

- **Load time**: from when the program starts reading the CSV to when the list is fully in memory
- **Search time**: from when the search function starts to when it returns results

Record the time at the start of each operation, record it again at the end, and print the difference. This is your measurement.

### Part B — Build the measurement table

Run the library with three different dataset sizes and fill in this table. Use the same search query each time so the results are comparable.

| Dataset size | Load time (seconds) | Search time (seconds) |
|-------------|--------------------|-----------------------|
| 10,000 books | | |
| 50,000 books | | |
| 100,000 books | | |

Run each measurement three times and use the middle value — the first run is sometimes faster or slower than usual due to the computer's own caching behaviour.

### Part C — Find the pattern

Look at your table. As the dataset doubles in size:
- Does load time roughly double? More than double? Stay the same?
- Does search time roughly double? More than double? Stay the same?

Write one sentence describing what you observe for each.

This pattern — how time grows as data grows — is one of the most important things an engineer learns to recognise. You do not need the formal theory yet. The numbers themselves will tell you what you need to know.

### Part D — Find the bottleneck

Compare your load time to your search time at 100,000 books.

Which is larger? By how much — 2 times? 10 times? 100 times?

The librarians at the school search the catalogue dozens of times per day. They only start the program once. Which problem — slow load or slow search — matters more for the daily experience of using the library? Write your answer and the reasoning behind it.

## Before You Start — Think About This

1. You run the search timing twice in a row with the same query. The second run is sometimes faster than the first. Why might that be? Does it mean the second measurement is more accurate, or less?
2. The load time measures how long it takes to read a file and build a list. The search time measures how long it takes to scan the list. Are these the same kind of operation? Would you expect them to scale the same way?
3. If 100,000 books causes the program to run out of memory and crash — what does that tell you? Record it as a measurement too: "program fails at X books with a memory error."

## When You're Stuck

- Python has a standard way to measure how much time has passed. Look up how to record a time before an operation and calculate the duration after it finishes.
- If you cannot get 100,000 books, estimate: measure at 10,000 and 50,000, then extrapolate what 100,000 would likely be based on the pattern you see.
- A measurement is only useful if you record the conditions: what computer, what dataset size, what query. Write all of this down alongside your numbers.

## Once It Works — Go Further

1. Python includes a built-in tool called `cProfile` that measures where time is spent across the whole program. Run it on your library and read the output. Which function consumes the most time? Does it match what you expected?
2. You measured time. Can you also measure memory? Look up how to check how much memory a Python program is using. How much memory does loading 10,000 books consume? 100,000?
