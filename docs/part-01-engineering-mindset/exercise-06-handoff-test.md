---
title: "1.6 The Handoff Test"
parent: Engineering Mindset
nav_order: 6
---

# Exercise 1.6 — The Handoff Test

## The Story

In December 2021, a small engineering team at a startup built a tool they called "the reconciler" — a Python script that compared two financial databases and reported mismatches. It worked perfectly.

In February 2022, the engineer who built it left the company. Nobody else had touched the code. Three months later, someone needed to run it.

There was no README. The script had no comments explaining which database it connected to or what format the input files needed to be in. The config file had parameter names that only made sense to the original author. Nobody could get it to run.

The tool was correct, well-written, and completely unusable.

This is called a handoff failure. Every piece of software you write will eventually be handed to someone else — a classmate, a colleague, a future version of yourself who has forgotten everything about this project. If that handoff fails, the software might as well not exist.

## What to Do

### The Handoff Test

Give your Mini Library project to one other person — a classmate, a sibling, anyone who has not seen it before.

They must be able to:
1. Get the program running using only your README
2. Add a book
3. Search for a book
4. Exit cleanly

You may not help them. You may only watch. Take notes on every moment they get confused, get stuck, or do something unexpected.

### After the Test

Write down everything you observed:
- What did they try to do that your README did not explain?
- What error did they get that you did not anticipate?
- Where did they look for information and not find it?
- What did they ask you to explain? (Each question is a gap in your documentation.)

Then fix each gap.

### If You Cannot Do a Live Test

If no one is available, do this instead:

Wait one week. Come back to your own Mini Library project and pretend you have never seen it before. Work only from the README and the comments in the code. Try to:
- Run the program
- Understand what each function does without reading the function body — only by reading its name and any comments
- Find where books are stored and why

Write down every question you had. Fix every gap.

### The Questions Your Project Should Answer

By the end of this exercise, your project should answer all of these without you present:

1. What does this program do? (one sentence)
2. What do I need installed to run it?
3. What command do I type?
4. What does a session with the program look like?
5. What files does it create, read, or expect to exist?
6. If it crashes, what is the most common reason?
7. What was the last thing that was changed and why?

Questions 1–5 belong in the README. Question 6 belongs in a Known Issues section. Question 7 is why we will need Git — but that comes in Part 3.

## Topics You Will Learn

- What "documentation completeness" means in practice
- The concept of the "bus factor" — how many people need to leave before a project becomes unmaintainable
- How to identify gaps between what you know and what you wrote down
- Why documentation is not just for others — it is for you in six months

## Before You Start — Think About This

1. Why does a programmer who wrote code always find their own documentation clear? What does that tell you about who you should be writing documentation for?
2. A classmate who has never used Python sits down with your project. What would they need that you have not provided? Is it your job to explain Python to them, or only how to use your program?
3. Some engineers say they write the README before they write the code. Why might that help them write better code?

## When You're Stuck

- Read your README out loud as if you are explaining the project to someone who has never heard of it. Every time you need to add words to make it make sense — those words need to be in the README.
- If your program produces an error message, it should be mentioned in the README so someone who sees it knows what to do.
- A README is not done when it is written. It is done when someone else successfully uses it.

## Once It Works — Go Further

1. Add a section to your README called **How This Project Is Organized** — one paragraph describing each file and what it does. Future readers will thank you.
2. Write a section called **What I Would Do Next** — two or three improvements you plan to make. This is especially valuable when you return to the project months later and need to remember where you left off.
