---
title: Real Data
nav_order: 7
has_children: true
---

# Real Data

So far, the library system works fine with 10 or 20 books. What happens with 10,000?

This section uses real data from Open Library to create real pain — slow startup, slow search, high memory usage. That pain is the reason databases exist.

## What to Observe

- How long does the program take to start?
- How long does a search take?
- How much memory does it use?
- What happens when two people use the library at the same time?

## The Questions

- Why is it slow — exactly what is the computer doing?
- Can it be fixed by optimising, or does the architecture need to change?
- What would the ideal storage system do that CSV cannot?

## Exercises

- [5.1 Import 10,000 Books](exercise-01-import-books.md)
- [5.2 Measure Performance](exercise-02-measure-performance.md)
- [5.3 Why Is It Slow?](exercise-03-why-is-it-slow.md)
- [5.4 The Ceiling](exercise-04-the-ceiling.md)