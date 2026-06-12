---
title: "6.2 Design the Schema"
parent: SQL as a Solution
nav_order: 2
---

# Exercise 6.2 — Design the Schema

## The Story

Before writing any SQL, engineers design the schema — the structure of the database. A schema defines what tables exist, what columns each table has, what type each column holds, and how the tables relate to each other.

A bad schema is very expensive to fix later. Getting it right at the start is worth the time.

This exercise is pencil-and-paper work. You will not touch a computer until Step 4.

## What to Do

### Step 1 — Identify the entities

An *entity* is a thing the system needs to remember. For the library, the entities are:

- **Book** — a physical book in the library
- **Member** — a person who has a library card
- **Loan** — the event of a member borrowing a book

Each entity becomes a table. Write one sentence describing each entity.

### Step 2 — Identify the attributes of each entity

For each entity, list the pieces of information the system needs to record. Example:

**Book**: title, author, year published, number of copies, ISBN

For each attribute, decide its type: text (string), number (integer or decimal), date, or yes/no (boolean). Be precise — `year` is an integer, not text.

### Step 3 — Identify the relationships

The three entities are connected:
- A **Loan** connects a **Book** to a **Member**
- A Member can have many Loans (past and present)
- A Book can have many Loans over time

Draw this on paper as three boxes (tables) with lines between them. On each line, write the relationship: "one member has many loans", "one loan belongs to one book."

### Step 4 — Write the schema in SQL

Translate your design into `CREATE TABLE` statements. The pattern is:

```
CREATE TABLE books (
    id        INTEGER PRIMARY KEY,
    title     TEXT NOT NULL,
    author    TEXT NOT NULL,
    year      INTEGER,
    copies    INTEGER DEFAULT 1
);
```

Write similar statements for `members` and `loans`. For `loans`, you will need foreign keys — columns that reference the `id` of another table.

### Step 5 — Verify your design

Answer these questions using only your schema (no data, just the structure):
1. Given a member's name, how would you find all books they have ever borrowed?
2. Given a book title, how would you find everyone currently borrowing it?
3. How would you find all books that have been borrowed more than 10 times?

If your schema cannot answer these questions, revise it.

## Topics You Will Learn

- Tables, columns, types (`TEXT`, `INTEGER`, `DATE`, `BOOLEAN`)
- Primary keys — every row has a unique identifier
- Foreign keys — how tables reference each other
- `NOT NULL` and `DEFAULT` — how to enforce data integrity
- Normalisation — why data should not be duplicated across tables

## Before You Start — Think About This

1. Should `author` be a separate table, or a text column in `books`? What is the trade-off? (Hint: what if an author's name is misspelled in 500 book records?)
2. The `loans` table needs to know both which book was borrowed and which member borrowed it. How do you express that relationship without copying the book's data into the loan record?
3. What is a primary key, and why does every table need one? What would happen if two books had the same `id`?

## When You're Stuck

- A foreign key is a column that holds the `id` of a row in another table. For example, `loans.book_id` holds the `id` of the borrowed book. This is how you link tables without copying data.
- `NOT NULL` means the column cannot be empty. Apply it to fields that are always required. Do not apply it to fields that are optional.
- Draw the schema on paper first. It is much faster to erase and redraw than to run `DROP TABLE` and start over.

## Once It Works — Go Further

1. Add a `categories` table (Fiction, Non-fiction, Science, History...) and link it to books. A book can belong to multiple categories — how does this change the schema? (Look up "many-to-many relationship" and "junction table.")
2. What would you need to add to the schema to track overdue books — books that have been borrowed for more than 14 days?
