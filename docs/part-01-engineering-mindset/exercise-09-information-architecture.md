---
title: "1.9 Information Architecture"
parent: Engineering Mindset
nav_order: 9
---

# Exercise 1.9 — Information Architecture

## The Story

Walk into a well-organized library — a real one, with books on shelves.

You are looking for a book about the history of the Indian Railways. You do not need to look at every book. You walk to the non-fiction section. You find the History aisle. You find the India sub-section. You scan the shelf. You find it in two minutes.

Now imagine the same library with no organization. All 50,000 books in one pile. Finding one book could take hours.

The librarian who organized those shelves made thousands of small decisions: What are the top-level categories? Does "Technology" go under Science or Business? Do biographies get their own section or live inside the relevant subject? Is there a "New Arrivals" shelf near the entrance?

These decisions are called **information architecture** — the structure you impose on information to make it findable.

Programmers make the same decisions every day. Where does this function go? What should this folder be called? How should this README be structured? What do I put at the top and what do I put at the bottom?

## What to Do

### Part A — The disorganized README

Here is a README with all the right information, but in the wrong order:

```
Mini Library

If the program crashes, it's usually because books.csv doesn't exist yet.
Just run the program once and it will create the file automatically.

Written by Amal. Started in November.

python library.py

You need Python 3.8 or higher installed.

A command-line program to manage a small collection of books.
You can add books, search for books, and list all books.

Searches are case-insensitive. So "sapiens" finds "Sapiens".

CSV format: title,author,year — one book per line.

Choose option 1 to add a book. You will be asked for title, author, and year.
The year must be a number.
```

All of the information above is useful. None of it is in the right order.

**Your task:** Rewrite this README so that a new user can read it from top to bottom and never need to scroll back up. Put the most important information first. Group related information together. Give each group a heading.

After you rewrite it, answer: what principle did you use to decide what goes at the top?

### Part B — Design the information hierarchy

Here is a list of documentation that a real library project might need:

- How to install the project
- What the project does (one sentence)
- How to run the project
- The CSV file format (column names and what they mean)
- Known bugs and limitations
- A list of planned future features
- How to run the tests
- The history of the project (who built it, when, why)
- How to contribute code changes
- A glossary of terms used in the project
- How to back up the data

Organize this list into a hierarchy. Decide:
- What goes in the README?
- What goes in a separate `docs/` folder?
- What gets its own file?
- What order do things appear in?

There is no single correct answer. But you must be able to justify every decision.

### Part C — Apply it to your own project

Look at your current Mini Library README and documentation. Using the principles you developed in Parts A and B:

1. Does your README answer the most important questions first?
2. Is related information grouped together?
3. Is there information that belongs in `docs/` rather than the README?
4. Is there anything missing entirely?

Rewrite and reorganize. When you are done, test it: give only your README to someone and see if they can use the project in 5 minutes.

## Topics You Will Learn

- Information architecture: the structure imposed on information to make it findable
- How to order information for a first-time reader (most important first)
- The difference between a README (quick start) and deeper documentation (`docs/`)
- How grouping, hierarchy, and headings help readers navigate

## Before You Start — Think About This

1. A table of contents helps a reader navigate a long document. When is a table of contents useful, and when is it unnecessary?
2. A programmer wrote a README that was technically complete but organized by what was easiest for the programmer to write, not what was easiest for the reader to read. How do these two perspectives differ?
3. The README for a library project serves two kinds of readers: someone who wants to *use* the program, and someone who wants to *modify* the code. Do they need the same information in the same order?

## When You're Stuck

- Ask: "What is the first question someone will have when they see this project?" The answer to that question goes first.
- Headings are navigation aids. If a reader can scan only the headings and understand the structure, your information architecture is working.
- When in doubt about what level of detail belongs somewhere, ask: "Would a first-time user need this in the first two minutes, or only later?"

## Once It Works — Go Further

1. Find a README on GitHub that you think is exceptionally well-organized. Write three sentences explaining what makes it work — what decisions did the author make about structure, order, and grouping?
2. Information architecture applies to code, not just documentation. A file called `library.py` that contains functions for books, members, transactions, and UI is organized by nothing. What would a better organization be? Write the new filenames and what each would contain. (You will implement this in Part 4.)
