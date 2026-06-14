---
title: "6.2 Design the Schema"
parent: SQL as a Solution
nav_order: 2
---

# Exercise 6.2 — Design the Schema

## The Story

The librarian sits down with you and explains the new requirement: "We need to track which students borrow which books. Right now I have a notebook where I write the student's name, the book title, the date borrowed, and the date returned. I need the computer to do this."

You pull out your `library.csv`. You could add columns: `borrowed_by`, `borrowed_on`, `returned_on`. But immediately a problem appears — a book can be borrowed many times. If you add those columns to the books row, you can only store the most recent loan. The entire history would be lost.

You could create a second CSV: `loans.csv`. But now when the librarian asks "what books does Priya currently have?" you would need to read the entire loans file and then look up each book in the books file — two scans, every time.

Before writing a single SQL statement, you need to design the structure — on paper.

## What to Do

### Part A — Identify what the system needs to remember

The library needs to remember three kinds of things:
- **Books** — each physical book
- **Members** — each registered student or teacher
- **Loans** — each event of a member borrowing a book

For each of these, write down every piece of information the library needs to record. Think like the librarian: what does she write in her notebook today?

For each piece of information, decide: is it text, a number, a date, or yes/no? Write it next to the field name. Being wrong here is expensive to fix later.

### Part B — Draw the connections

Take a blank sheet of paper. Draw three boxes, one for each of the three things above. Inside each box, list the fields you identified in Part A.

Now draw lines between the boxes:
- A loan is connected to exactly one book
- A loan is connected to exactly one member
- A member can have many loans
- A book can have many loans over time

On each line, write the relationship in plain English: "one member has many loans," "one loan belongs to one book."

This drawing is your design. Keep it beside you for the rest of Part 6.

### Part C — Solve the connection problem

Here is the central challenge: when you record a loan, you need to say *which book* and *which member*. You cannot copy all the book details into the loan record — if the book's title is corrected later, you would have wrong data in every loan.

Think: what is the minimum information you need in the loan record to identify the book, without copying the book's data?

Write your answer. Then extend your drawing from Part B to show how this connection works.

### Part D — Verify your design answers real questions

Using only your drawing (no computer, no data), trace the path to answer each of these questions:
1. Which books does Priya currently have borrowed?
2. How many times has "To Kill a Mockingbird" been borrowed this year?
3. Which members have never returned a book on time?

For each question: can your design answer it? If not, what is missing?

## Before You Start — Think About This

1. Should `author` be a column in the books table, or a separate table of its own? Think about what happens if the same author's name is spelled differently in 200 book records. Which approach makes it easier to fix?
2. Every row in every table needs a unique identifier. Why? What would happen if two books had the same identifier and you tried to record a loan for one of them?
3. The loan record connects a book to a member. The loan does not need to store the book's title or the member's name — it only needs to reference them. Why is this better than copying?

## When You're Stuck

- A *primary key* is a unique identifier for each row in a table — like a library card number. No two rows can share one.
- A *foreign key* is how one table references a row in another table. The loan record stores the book's unique identifier, not the book's data. This is the connection.
- `NOT NULL` means the field must always have a value — you cannot save a row with that field empty. Which fields in your design must always have a value? Which are optional?
- Draw first. It is much faster to erase than to undo a bad database design.

## Once It Works — Go Further

1. The library wants to track book categories: Fiction, Non-fiction, Science, History. A book can belong to more than one category. How does this change your drawing? (Look up "many-to-many relationship" and "junction table.")
2. What would you need to add to know when a loan is overdue? The library's rule is: books must be returned within 14 days. Walk through your design and describe the change.
