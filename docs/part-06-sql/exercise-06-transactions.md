---
title: "6.6 Transactions"
parent: SQL as a Solution
nav_order: 6
---

# Exercise 6.6 — Transactions

## The Story

It is a busy Tuesday morning. A student comes to the library counter to return a book. The librarian uses the system to record the return:

1. Mark the loan record as returned (set the `returned_date` to today)
2. Update the book's `available_copies` count by adding 1

The librarian clicks "Return Book." The first update runs — the loan is marked as returned. Then, just as the second update is about to run, the laptop's power cable is knocked loose. The screen goes dark.

When the librarian restarts the computer and opens the system, the loan shows as returned — but the book's `available_copies` count was never updated. The library now shows zero copies available for a book that is sitting on the shelf. Every student who tries to borrow that book will be told it is checked out, even though it is not.

This is a real problem that happens when related database changes are made one at a time, with no safety net. It is the last major problem from your requirements list in Exercise 6.1 — the one you wrote as "either the full change is saved or nothing changes."

That capability has a name: a **transaction**.

## What to Do

### Part A — Experience the problem

Build a small version of the broken scenario:
- Write a Python function called `return_book(loan_id, book_id)` that performs both updates — mark the loan returned, then update the copy count
- Between the two database operations, add a line that deliberately crashes the program (raise an exception, or use `sys.exit()`)
- Run the function and observe: which update ran? What is the state of the database now?
- Check the database in DB Browser. Is the data consistent?

Write down what you find. This is the bug that transactions are designed to prevent.

### Part B — Understand what "all or nothing" means

Before writing any transaction code, think through what you actually want:

"When a student returns a book, either *both* of these things happen — the loan is marked returned AND the copy count is updated — or *neither* happens. There must never be a state where one happened and the other did not."

This is the guarantee a transaction provides. If anything goes wrong between the first and second operation, the database automatically undoes the first one, as if neither had run.

Write your own version of this guarantee for the "borrow a book" scenario. What two things must happen together when a student borrows a book? What would the broken state look like if only one happened?

### Part C — Fix the function using a transaction

Rewrite `return_book(loan_id, book_id)` to use a transaction. Look up how SQLite handles transactions in Python — the key operations are beginning a transaction, committing it when both updates succeed, and rolling back if anything fails.

Test it by introducing the crash again (the exception between the two updates). Run the function. Then check the database: what happened to the first update this time?

### Part D — Apply to the borrow function

Find the part of your library program that records a new loan (when a student borrows a book). This probably updates the loans table and reduces the available copy count. Wrap those operations in a transaction too.

Think through: what should happen if the student tries to borrow a book and there are zero copies available? Should the transaction even start? Or should you check availability before the transaction begins?

## Before You Start — Think About This

1. The scenario above has two database updates that must succeed or fail together. Can you think of another scenario in the library where two operations must happen together — where a partial success would leave the data in a broken state?
2. The bank analogy: transferring money from one account to another requires subtracting from one account and adding to another. What would happen at the bank if the power failed between those two operations? How does a bank prevent this?
3. In the Python `sqlite3` module, every database connection has a concept of "autocommit" — where each operation is saved immediately. Transactions turn this off temporarily, batching multiple operations into one. Why is autocommit a problem for multi-step operations?

## When You're Stuck

- A transaction in SQLite begins when you start a group of related operations, and ends when you either `COMMIT` (save all of them) or `ROLLBACK` (undo all of them). Look up these commands in the SQLite documentation.
- In Python's `sqlite3` module, look up how to begin and commit a transaction explicitly. The default behaviour may already wrap operations in transactions — find out which behaviour your code is using.
- A `try...except...finally` block is useful here: try to do both updates, commit if both succeed, rollback in the `except` if anything fails.

## Once It Works — Go Further

1. Look up the four properties of database transactions: **ACID** (Atomicity, Consistency, Isolation, Durability). Match each property to a real library scenario — what does "isolation" mean when two students are borrowing books at the same time?
2. The transaction guarantee is "all or nothing." But what if "all" partially succeeds, then the second operation fails, and the rollback itself fails? Look up what databases do to protect against rollback failure (look up "write-ahead logging" or "WAL").
