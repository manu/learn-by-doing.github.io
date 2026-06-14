---
title: "1.8 Naming Consistency"
parent: Engineering Mindset
nav_order: 8
---

# Exercise 1.8 — Naming Consistency

## The Story

A team of three engineers builds a library system over six months. Each engineer names things slightly differently:

- Engineer A calls it a `book`
- Engineer B calls it an `entry`
- Engineer C calls it a `record`

In the code, you find `add_book()`, `create_entry()`, and `save_record()` — all doing the same thing to the same object. In the database, the table is called `items`. In the API, it's called a `title`. In the README, it's called a `publication`.

Six different words. One concept.

Every time a new engineer joins the project, they must learn: "what does 'entry' mean here? Is it the same as 'record'? Is it the same as 'book'?" That translation tax is paid by every person, every day, forever.

This is called **terminology drift** — and it happens quietly, one small decision at a time.

## What to Do

### Part A — Audit the Mini Library vocabulary

Read through your entire Mini Library project — the Python code, the README, the CSV headers, any comments or notes you have written. Make a list of every noun used to refer to a book in the library:

- Function names (what word do they use?)
- Variable names (what word do they use?)
- CSV column headers (what are they called?)
- README text (what word does it use?)
- Print statements and messages to the user

You will likely find at least two or three different words. Write them all down.

### Part B — Choose one word. Use it everywhere.

Pick one word for the thing a library contains. Consider:
- Is it a `book`? (accurate, but what about DVDs, magazines, audiobooks?)
- Is it an `item`? (generic, but covers everything)
- Is it a `resource`? (very generic)

There is no universally correct answer. But you must choose **one word** and use it **everywhere**:
- Function names
- Variable names
- CSV column headers
- README
- Print messages
- Comments

Make every change. Test that the program still works after each rename.

### Part C — Write a vocabulary decision

In your README, add a section called **Glossary** with one entry:

> **[your word]** — A single item in the library collection (book, DVD, audiobook, etc.)

This documents your decision so the next person who works on this project does not invent their own word.

### Part D — Naming patterns

Now look at your function names for a pattern. A function that adds an item to the library, one that removes an item, and one that searches for an item should follow the same verb pattern:

- `add_book` / `remove_book` / `search_book` (verb + same noun)
- OR: `book_add` / `book_remove` / `book_search` (same noun + verb)

Pick one pattern and make all functions follow it. Mixed patterns are harder to remember and harder to autocomplete in a code editor.

## Topics You Will Learn

- Terminology drift and how it accumulates over time
- The concept of a project vocabulary (ubiquitous language)
- Consistent naming patterns for functions (verb+noun vs noun+verb)
- How naming inconsistency creates a hidden cost for every reader

## Before You Start — Think About This

1. The word `data` appears in almost every codebase. Is `data` a good variable name? What information does it carry that `books`, `members`, or `transaction_log` do not?
2. Why do inconsistent names happen in the first place? When does a developer reach for a different word, and what could they do instead?
3. If you are writing code alone, does naming consistency still matter? What happens six months later when you re-read it?

## When You're Stuck

- Renaming a function in Python also requires changing every place that calls it. Search for the old name first: find every use before changing any.
- Start with the most fundamental word (what is the main thing the library stores?) before moving on to less central concepts.
- CSV column headers are the most often overlooked. If the CSV says `title,author,year` but your code calls them `name`, `writer`, `date` — you have already introduced drift.

## Once It Works — Go Further

1. The concept of consistent vocabulary has a name in software design: **Ubiquitous Language** (coined by Eric Evans). Look it up. In two or three sentences, explain what it means and why it matters for a project with more than one developer.
2. Pick one more concept in your Mini Library (members, transactions, searches) and audit it the same way you audited book/item/entry/record. Does it have the same drift problem?
