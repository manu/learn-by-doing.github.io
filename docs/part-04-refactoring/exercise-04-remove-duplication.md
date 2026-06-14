---
title: "4.4 Remove Duplication"
parent: Refactoring
nav_order: 4
---

# Exercise 4.4 — Remove Duplication

## The Story

Six months after the library launched, the school decides that any book published before 1900 should be marked as "archival" and cannot be borrowed. You search for where the year check lives in the code.

You find it in five places.

You update four of them. You miss the fifth — it is in a part of the code you did not know existed. Three weeks later, a student borrows an 1887 book that should have been restricted. Nobody can figure out why, because four of the five checks work correctly.

This is the cost of duplication. Not the typing. The divergence.

When the same logic exists in two places, those two copies will eventually disagree — because one will be updated and the other will not. The program behaves differently in two situations that should be identical, and nobody knows why. Bugs caused by diverged duplicates are some of the hardest to find because the code *looks* correct everywhere you look.

The principle that prevents this is called **DRY — Don't Repeat Yourself**: every piece of knowledge should have exactly one representation in the system.

## What to Do

### Part A — Hunt for the duplicates

Read through your library modules. Duplication is not always obvious. Look for three kinds:

**Same logic in different places** — two functions that do the same thing, or near-enough the same thing. Maybe one is named `find_book` and another `get_book` and they are nearly identical.

**Same structure with different values** — two sections that follow the same pattern but with different data. Validating a year follows the same pattern as validating that a title is not empty: check a condition, return an error message, otherwise continue.

**Same value written out multiple times** — the string `"library.csv"` appears in three functions. The year threshold `1900` appears in five places. These are called *magic values*: numbers or strings with meaning, written directly into the code instead of being named.

Write down every example you find. Do not fix anything yet.

### Part B — The divergence test

For each piece of duplication you found, ask: if the requirement changed — if the filename changed, if the year threshold changed — how many places would you need to update?

Count them. Write the number next to each duplication. That number is the risk.

### Part C — Remove one duplication

Start with the most dangerous one — the highest count from Part B.

Common fixes:
- **Two functions that do the same thing** → decide which name is better, delete the other, update every caller to use the surviving one
- **Same structure with different values** → extract one function where the differing part becomes a parameter
- **Repeated value** → give the value a name and define it once; every use refers to the name

After removing the duplication, make a change to the single remaining version. Verify that the change is reflected everywhere. If you have to change anything else — you missed a copy.

### Part D — Where duplication is acceptable

DRY is a principle, not a law. Two pieces of code that look similar but represent genuinely different ideas should stay separate — combining them would create a function so general that nobody can understand what it does.

Look at your list of duplicates. For any you decided NOT to remove, write one sentence explaining why the similarity is superficial and the ideas are genuinely different.

## Before You Start — Think About This

1. In the story above, the bug was caused by updating four of five copies. How would the same requirement change have gone if the year check existed in exactly one place?
2. When is a little duplication acceptable? Some engineers say: "Duplicate once, extract on the third time." Why might that be a sensible rule?
3. Naming a value `MINIMUM_YEAR = 1900` instead of writing `1900` directly — this is not just about DRY. What else does a named constant give you that a raw number does not?

## When You're Stuck

- If two functions are nearly identical, list what is different. If the difference is small and regular, it becomes a parameter. If the difference is large and irregular, they might not really be duplicates.
- Named constants go at the top of the relevant module in uppercase: `LIBRARY_FILE = "library.csv"`. Every place that previously used the raw string now uses the name.
- Over-removing duplication is a real risk. If extracting a shared function makes the function so abstract it has no clear meaning, the duplication was better.

## Once It Works — Go Further

1. After removing duplication, introduce the year-threshold change from the story (change the threshold from 1900 to 1850). How many places did you have to update? Compare this to what you wrote in Part B.
2. Write a short rule for yourself: "I will consider removing duplication when \_\_\_\_. I will leave it when \_\_\_\_." This becomes part of your engineering judgment.
