---
title: "5.4 The Ceiling"
parent: Real Data
nav_order: 4
---

# Exercise 5.4 — The Ceiling

## The Story

The librarian has been patient. She has watched you optimise, measure, and experiment for a week. The library is faster than it was — but still nowhere near fast enough.

"What if we just buy a faster computer?" she asks.

It is a reasonable question. If the program is slow because the computer is slow, a better computer would fix it. But you have a feeling that is not the problem. The problem is not the hardware. It is the approach.

You are about to discover the concept of an **architectural ceiling** — a limit that cannot be passed by making the existing system faster, only by changing the design of the system itself.

## What to Do

### Part A — The faster computer thought experiment

Imagine you buy a computer 10 times faster than your current one. The program now runs 10 times faster too.

At 100,000 books:
- Your current search takes 1 second. On the new computer: 0.1 seconds. Is that fast enough?
- At 1,000,000 books (ten times more data): the search is back to 1 second on the new computer. What happens at 10,000,000?

Fill in this table for your current search algorithm on a hypothetical "10× faster computer":

| Books | Time on current computer | Time on 10× faster computer |
|-------|------------------------|---------------------------|
| 100,000 | (your measurement) | ÷ 10 |
| 1,000,000 | × 10 (estimate) | |
| 10,000,000 | × 100 (estimate) | |
| 100,000,000 | × 1000 (estimate) | |

At what point does even a 10× faster computer fail to keep up?

### Part B — The simultaneous users problem

The librarian mentions that sometimes two students search for books at the same time. She would like to add computers in two classrooms, both connected to the same library.

Think through what would happen:

1. Student A searches for "history" at the exact same moment Student B searches for "science".
2. Both programs load the CSV into their own memory.
3. Student A's teacher asks them to add a new book. Student A adds it and saves.
4. Student B's teacher also asks them to add a book at the same time. Student B adds it and saves.

What has happened to the CSV file? Do both new books exist in the file? Does one overwrite the other? Is there a version with neither book, only the original 100,000?

Try this. Open two terminal windows. Run the library program in both. Add a book in one. Without closing either, add a book in the other. Look at the CSV. What do you find?

Write down exactly what happened and why.

### Part C — The multi-field search problem

The librarian has a new requirement: "I need to find all books borrowed by a specific student, across all their transactions, sorted by the date they borrowed them."

With your current CSV library:
1. You have `library.csv` — books and their details
2. You have no transaction log

To add transaction tracking, you would need a second CSV: `transactions.csv` with columns for student name, book title, and date.

To answer "all books borrowed by Priya":
- You read all of `transactions.csv` (100,000 rows)
- For each transaction belonging to Priya, you look up that book in `library.csv` (another scan)

How many total operations does this require for 100,000 books and 50,000 transactions?

Write down the number. Is this feasible?

### Part D — Write the ceiling

Write one paragraph summarising the three ceilings you discovered:
1. Speed: the CSV approach cannot be made fast enough by optimising Python
2. Concurrent access: two users writing to the same CSV at the same time causes data loss
3. Relationships: connecting data across multiple CSVs requires scanning everything multiple times

These are not fixable within the CSV architecture. They require a different system.

This paragraph, combined with the one you wrote at the end of Exercise 5.3, is your complete case for why the library needs a database.

## Before You Start — Think About This

1. The problem of two people writing to the same file at the same time is called a **race condition**. Without a system that prevents this, which write wins? Is the loser's data simply gone?
2. A database runs as a separate service — a program that is always running, that your library program connects to. Why does this help with the simultaneous users problem?
3. The word "transaction" in Part C (a student borrowing a book) is different from the word "transaction" in databases (an atomic unit of operations). How are they related? What does a database "transaction" guarantee that two separate CSV writes cannot?

## When You're Stuck

- For Part B, the experiment works best if you add books in both windows in quick succession and then look at the CSV before closing either program. The result may vary — sometimes one write wins cleanly, sometimes the file is corrupted. Both outcomes are informative.
- For Part C, you do not need to build the transaction system — just design it on paper and calculate the operations.

## Once It Works — Go Further

1. The problem in Part B has a name: a **write conflict** or **race condition**. Look up how databases solve this (the answer involves locking). In one sentence, explain what "locking" means in plain language.
2. Part 6 will introduce SQL databases. Before you start, write down three questions you want Part 6 to answer based on the ceilings you discovered here.
