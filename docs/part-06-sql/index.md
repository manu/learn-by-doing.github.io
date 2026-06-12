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

- [Why CSV Hurts](exercise-01-why-csv-hurts.md)