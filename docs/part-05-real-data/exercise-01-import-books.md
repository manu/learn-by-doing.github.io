---
title: "5.1 Import 10,000 Books"
parent: Real Data
nav_order: 1
---

# Exercise 5.1 — Import 10,000 Books

## The Story

The school receives a letter from a charity. They are donating their catalogue to the school library — 10,000 books, exported from the Open Library database, in a file called `books-10k.csv`.

The librarian hands you a USB drive and says: "Can you load all of these into the system?"

You look at your Mini Library. It has handled 20 books comfortably. You have never tried it with more than 50. You plug in the USB drive, copy the file, and run the import.

Something is wrong. The program starts. And starts. And keeps starting. The menu has not appeared yet. You wait.

You have just experienced what engineers call a **scaling problem** — a program that works perfectly at small size, breaks at large size, without any bug being introduced.

## What to Do

### Part A — Build the import script

Write a separate script called `import_books.py`. It is not the library program — it is a one-time tool that reads the donation file and prepares it for the library.

Before writing any code, answer these questions:
1. What format is the donation file in? (Tab-separated? Comma-separated? What columns does it have?)
2. What format does your library expect? (What columns does `library.csv` use?)
3. What should happen when a row in the donation file has a missing title, or a year that is not a number, or a character the program cannot read?

Write your answers before opening a text editor. These are your requirements.

### Part B — Run the library with 10,000 books

Once the import is done, start the library program and time how long it takes for the menu to appear. Use a phone stopwatch — count from the moment you press Enter to the moment the menu is visible.

Write the number down.

Then search for a common word — "the", or "history", or "India". Time how long the search takes to return results.

Write that number down too.

### Part C — Observe, do not fix

You may be tempted to improve the code. Do not. Not yet.

Instead, write down everything you observe:
- How long did startup take?
- How long did search take?
- What did it *feel* like to wait for each? ("It felt slow" is a valid observation, but also say how slow: "I counted to 4 before the results appeared.")
- What would a real librarian think if they used this program?

These observations are data. You will use them in Exercise 5.2.

## Before You Start — Think About This

1. The library program loads the entire CSV into a Python list when it starts. With 10,000 books, roughly how many book dictionaries does that list hold? What does each dictionary contain?
2. When you search for "history", the program checks every single book to see if "history" appears in its title. With 10,000 books, how many checks does one search require?
3. The import script reads one file and writes another. Why is it better as a separate script rather than a button inside the library menu?

## When You're Stuck

- Open the donation file in a text editor before writing any code. Look at the first few lines. What character separates the columns? Are there column headers on the first line? How many columns are there?
- Some rows may have unusual characters, or more columns than expected, or fewer. Think about how to handle these gracefully rather than crashing.
- Your import script does not need to be fast or elegant. It runs once. Correctness matters more than speed here.

## Once It Works — Go Further

1. Import 50,000 books instead of 10,000. Time the startup and search again. Did the times double? More than double?
2. Look at the data that was imported. Are there books with missing years? Duplicate titles? What would a real library need to do about these — and what does that tell you about data quality?
