---
title: "4.1 The 300-Line File"
parent: Refactoring
nav_order: 1
---

# Exercise 4.1 — The 300-Line File

## The Story

The Mini Library started at 50 lines. After adding borrow tracking, delete, search improvements, and error handling, it is now over 300 lines. It still works — every test passes, every feature is there. But something has changed.

Finding where the search logic lives requires scrolling. Changing the CSV format means editing in three different places. Adding a new feature means reading 300 lines to understand what already exists. Two functions share the same helper logic but neither calls the other.

The code has accumulated what engineers call *technical debt* — not bugs, but complexity that makes future work slower and riskier. Refactoring is paying that debt back.

## What to Do

### Step 1 — Read before you touch

Read the entire file from top to bottom without changing anything. As you read, write down:

1. Every place where you have to re-read a section because it was not clear the first time
2. Every function that is longer than 20 lines
3. Every comment that explains *what* the code does (rather than *why*) — these are signs the code is not self-explanatory
4. Every piece of logic that appears more than once

Do not start refactoring yet. This reading is the diagnosis.

### Step 2 — Identify one thing to improve

From your list, pick the single most confusing or tangled section. Not the biggest problem — the most contained one. Refactoring is safest when done in small steps with a test after each step.

### Step 3 — Refactor that section

Apply one of these techniques:
- **Extract function**: Move a block of logic into its own named function
- **Rename**: Rename a variable or function to better describe what it holds or does
- **Remove duplication**: If two sections do nearly the same thing, write one function and call it from both places

After each change, run the program and verify it behaves identically to before.

### Step 4 — Write down what changed

For each refactoring move, write one sentence: what you changed and why it makes the code clearer. This is not a comment in the code — it is a note for yourself about the *decision*.

## Topics You Will Learn

- How to read unfamiliar code methodically
- Extract function — the most important refactoring technique
- When a comment is a sign of a naming problem
- The rule: change one thing at a time, verify after each change

## Before You Start — Think About This

1. Refactoring means the program's behaviour does not change. How do you verify behaviour has not changed if you have no automated tests? What would you check manually?
2. If a function is 50 lines long, does that automatically mean it should be split? What is the right question to ask instead of "how long is it"?
3. You find two sections of code that do almost the same thing — but not exactly. Is it better to merge them into one function (risking making it complicated) or leave the duplication? How do you decide?

## When You're Stuck

- If you are not sure whether a refactoring is safe, add a temporary `print` statement before and after to check the output is unchanged.
- "Extract function" means: take a block of code, give it a name, move it to its own function, and call that function from where the block used to be. The program does exactly the same thing — it just has a name for that block now.
- Small steps are safer than large steps. If you try to refactor everything at once and something breaks, you will not know which change caused it.

## Once It Works — Go Further

1. After refactoring, measure the length of your longest function. What is it now? Set a personal rule for the maximum length a function should be in your projects.
2. Find a section of code that has a comment explaining what it does. Refactor the code so the comment is no longer needed — the code should explain itself through naming.
