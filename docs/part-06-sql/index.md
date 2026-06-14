---
title: SQL as a Solution
nav_order: 8
has_children: true
---

# SQL as a Solution

SQL is introduced only after the pain of CSV at scale has been experienced.

A database is not just a faster CSV. It is a different model for thinking about data — with schemas, relationships, indexes, and transactions.

## Key Concepts

- Schema design
- Relationships between tables
- Joins
- Indexes — why search becomes fast
- Transactions — all-or-nothing operations

## The Goal

Understand *why* SQL exists. Not memorize syntax.

## Library Schema

```
books        → id, title, author, year
members      → id, name, email
transactions → id, book_id, member_id, date, returned
```

## Exercises

- [6.1 Why CSV Hurts](exercise-01-why-csv-hurts.md)
- [6.2 Design the Schema](exercise-02-design-schema.md)
- [6.3 Create Tables and Migrate](exercise-03-create-and-migrate.md)
- [6.4 Search and Join](exercise-04-search-and-join.md)
- [6.5 Indexes](exercise-05-indexes.md)
- [6.6 Transactions](exercise-06-transactions.md)