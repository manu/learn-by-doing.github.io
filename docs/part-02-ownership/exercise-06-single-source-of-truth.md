---
title: "2.6 Single Source of Truth"
parent: Ownership and Responsibility
nav_order: 6
---

# Exercise 2.6 — Single Source of Truth

## The Story

Your Mini Library keeps books in two places at the same time:

1. In memory — a Python list, fast to read and update during the session
2. In a file — a CSV on disk, so the data survives when the program closes

When the program starts, it reads from the file into the list. When books are added, it appends to the list. But does it also save to the file? When does it save?

Now answer this honestly:

- If someone adds a book and the program crashes before saving — is that book in the file?
- If you add a book, then open the CSV file in a text editor, and then add another book — what happens when the program saves?
- If you edit the CSV file directly while the program is running, and then search for the book you added — will you find it?

These are questions about **consistency**. When data lives in two places, the two copies can silently disagree. Which one is correct? Which one do you trust?

This is the problem the **Single Source of Truth** principle solves: for any given piece of data, there is exactly one place where its authoritative value is stored. Everything else is either a cache (a copy for speed) or derived from the source.

## What to Do

### Part A — Find where data lives twice

Map out every place in your Mini Library where the same data exists in more than one form:

- Books in the in-memory list vs books in the CSV file
- The total count of books (if you store it separately anywhere)
- Anything else you find

For each duplicate, answer: if these two copies disagree, which one is correct?

### Part B — Design the contract

Decide: **which is the source of truth — memory or file?**

Option 1: File is the source of truth
- Every add/remove saves to file immediately
- The in-memory list is just a cache to avoid reading the file every time
- On startup, memory is populated from the file

Option 2: Memory is the source of truth during a session
- Changes go to memory first
- The file is updated at specific points (on exit, on every change, on a timer)
- There is a clear rule about when the file and memory are guaranteed to match

Pick one option. Write down the rule in one sentence: "The source of truth is \_\_\_\_ because \_\_\_\_. The \_\_\_\_ is updated when \_\_\_\_."

### Part C — Implement the contract

Rewrite your Mini Library to follow your chosen rule consistently:

- Every function that modifies books must follow the rule
- There should be no code path where the rule is violated
- If the program crashes mid-operation, what state are you in? Is it recoverable?

Test the following scenario:
1. Add three books
2. Open the CSV in a text editor
3. Check that the CSV matches the in-memory list exactly (or check that it matches at the point your rule says it should)

### Part D — The harder question

What if the program crashes between adding the book to memory and saving it to the file? The book exists in memory but not in the file. After restart, the book is gone.

This is called a **consistency failure**. Databases solve this with transactions — a way of saying "do all of this, or none of it." You will study transactions in Part 6 (SQL).

For now, think about it: if you save to the file *before* adding to the in-memory list, and then the program crashes — what state are you in? Is it better or worse than the other order?

Write down which order you chose and why.

## Topics You Will Learn

- Single Source of Truth — one authoritative location for each piece of data
- The difference between a source and a cache
- What "data consistency" means and how inconsistency happens
- Why the order of operations matters when writing to multiple places

## Before You Start — Think About This

1. A phone syncs contacts with the cloud. Your phone has a copy, the cloud has a copy. If you edit a contact while offline, and someone else edits the same contact online — which version is correct? How do you know?
2. In your Mini Library, if you change a book's year by editing the CSV directly, the in-memory list does not update. Is this a bug, or is it expected behavior? What does your "source of truth" decision say about this case?
3. Some programs save every change immediately (like Google Docs). Others save only when you click Save (like an older word processor). What are the trade-offs of each approach?

## When You're Stuck

- "Save on every change" is the simplest rule — after every add or remove, write the full list to CSV. It is slower (especially with many books) but always consistent.
- "Save on exit" is faster but risky — a crash loses all unsaved changes. You need a way to handle the case where the program did not exit cleanly.
- If you are not sure which rule to use, use "save on every change" for now. You will revisit this when you move to a proper database in Part 6.

## Once It Works — Go Further

1. Add a "reload from file" option to your main menu. This re-reads the CSV and replaces the in-memory list. Why would this be useful? When would you need it?
2. What would happen if two people ran your Mini Library at the same time, both adding books to the same CSV file? This is the problem databases solve with locking. Think about what the damage would look like and write it down — you will understand the solution in Part 6.
