---
title: "1.3 Write a README"
parent: Engineering Mindset
nav_order: 3
---

# Exercise 1.3 — Write a README

## The Story

Imagine you find a USB drive with a folder called `library-project`. Inside are several Python files, a CSV, and no explanation of any kind. You spend an hour trying to figure out which file to run, what the program does, and what you need installed before it will work.

Now imagine the folder has a file called `README.md` that answers all of those questions in two minutes.

The README is the first thing anyone reads when they encounter your project. It is your project's front door. A good README does not document every line of code — it answers exactly the questions a new person needs to start using your work.

## What to Build

Write a `README.md` file for your Mini Library project. It must answer these five questions — and only these five:

1. **What does this program do?** — One sentence. Not a paragraph.
2. **How do I run it?** — The exact command to type.
3. **What do I need installed first?** — Python version, any libraries.
4. **What files does it create or expect?** — Does `library.csv` need to exist first, or does the program create it?
5. **What does a typical session look like?** — Paste one short example of the program running.

```
# Mini Library

A command-line program to manage a small book collection.

## How to Run

    python library.py

## Requirements

Python 3.8 or higher. No external libraries needed.

## Files

The program reads from and writes to `library.csv` in the same folder.
The file is created automatically on first run.

## Example

    === Mini Library ===
    1. Add book
    2. List all books
    3. Search by title
    4. Quit

    Choose an option: 1
    Title: Sapiens
    Author: Yuval Noah Harari
    Year: 2011
    Book added.
```

## Topics You Will Learn

- Markdown formatting (headings, code blocks, lists)
- What belongs in a README and what does not
- Writing for an audience who is not you
- The concept of "minimum viable documentation"

## Before You Start — Think About This

1. Who is the audience for your README? Is it someone who knows Python well, or someone who has never used it? How does that change what you write?
2. Every word in a README that is not necessary is a word the reader has to process before finding what they need. What would you cut?
3. What is the difference between documentation that explains *what* the code does versus documentation that explains *how to use* the program? Which does a README do?
4. If your program requires no installation and runs with just `python library.py` — do you still need a Requirements section? Why or why not?

## When You're Stuck

- Write the README as if you are leaving instructions for yourself two years from now, when you have completely forgotten this project.
- Test it: give the README to someone who has not seen your project and ask them to run the program using only the README as a guide. Where did they get stuck? Fix those places.
- Markdown is simple: `# Heading`, `## Subheading`, backticks for `inline code`, triple backticks for code blocks.

## Once It Works — Go Further

1. Add a **Known Issues** section — one or two things your program does not handle well (for example: what happens if the user enters a year that is not a number?).
2. Add a **Future Plans** section — two things you would add if you had more time. This is useful when you come back to the project months later.
3. Look at the README of a popular open-source project on GitHub (try `requests` or `flask`). Write down three things their README does that yours does not, and decide whether those things would be useful for your project.
