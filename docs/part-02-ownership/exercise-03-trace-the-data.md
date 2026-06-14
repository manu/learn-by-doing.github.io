---
title: "2.3 Trace the Data"
parent: Ownership and Responsibility
nav_order: 3
---

# Exercise 2.3 — Trace the Data

## The Story

A bug report comes in: "Sometimes the library shows 8 books, sometimes 7. I didn't delete anything."

The developer opens the code. There are six functions. Any one of them could be responsible. She spends two hours tracing through the code before finding the problem: a function that was supposed to *display* books was also *removing duplicates from the list in place* as a side effect of the display.

The root cause was not the bug itself. The root cause was that nobody could answer the question: **where does the books list come from, and what is allowed to change it?**

This is the problem explicit data flow solves. In a program with explicit data flow, you can draw an arrow from where every piece of data is created to every place it is used. You can see, at a glance, who reads it and who changes it.

## What to Do

### Part A — Draw the current data flow

Open your Mini Library. For each piece of data below, trace it through the program and answer the three questions in writing:

**The books list:**
1. Where is it created?
2. Which functions read it?
3. Which functions modify it?

**A single book (one dictionary):**
1. Where is it created?
2. Which functions receive it?
3. Which functions modify it?

**The search term (what the user typed):**
1. Where does it enter the program?
2. Which functions receive it?
3. Which functions use it to filter or display data?

Draw this as a diagram — arrows from source to each consumer. Use paper or a simple text diagram. If you cannot draw it, your program's data flow is not explicit enough.

### Part B — Find the invisible flows

Hidden data flow happens when:
- A function modifies data it received without the caller knowing
- A function reads data from a global rather than a parameter
- A function both returns a value AND modifies its input

Check your Mini Library for all three patterns. Write down every example you find.

### Part C — Redesign for visibility

Pick the worst example you found in Part B — the piece of data whose flow is hardest to trace. Redesign that part of the program so the data flow is visible:
- The function receives the data it needs as a parameter
- The function returns the data it changed
- The caller can see exactly what enters and what comes out

You are not changing what the program does. You are making it possible for a reader to follow the data with their eyes.

## Topics You Will Learn

- Explicit vs implicit data flow
- How to read a program and trace data from source to use
- What "hidden" data flow looks like and why it causes bugs
- How parameters and return values make data flow visible

## Before You Start — Think About This

1. In a program with only global variables, how many places could change a value? How does that make debugging harder?
2. If a function takes a list as a parameter and also modifies it in place, the caller receives the modified list back through the return value AND through the original variable. Is this a problem? Why might it cause confusion?
3. In a well-designed program, can you understand what a function does without reading its body — just by reading its name, parameters, and return type? Does your Mini Library achieve this?

## When You're Stuck

- Start with the most important data in your program: the books list. Every function that touches it should be visible in your diagram.
- "Invisible" modification looks like: `def show_books(books): books.sort()` — the sort modifies the caller's list even though the function is named "show".
- If you cannot trace a piece of data from where it is created to where it is used, that is a signal to redesign, not to debug harder.

## Once It Works — Go Further

1. After drawing the diagram, count: how many functions read the books list? How many modify it? If more than 2-3 functions modify it, you have a design problem worth fixing.
2. The pattern where one piece of data has exactly one place where it can be changed is called a **single owner**. In your redesigned version, which function owns the books list?
