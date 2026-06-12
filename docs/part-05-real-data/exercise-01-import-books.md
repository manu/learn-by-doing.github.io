---
title: "5.1 Import 10,000 Books"
parent: Real Data
nav_order: 1
---

# Exercise 5.1 — Import 10,000 Books

## The Story

The school library has just received a donation: the complete Open Library dataset — a free, publicly available catalogue of millions of books. The librarian wants to import 10,000 of them into the system.

Your Mini Library currently handles 10 to 20 books comfortably. What happens when you give it 10,000?

This exercise will not feel like a success. It is designed to feel like a problem. That problem is what the next several exercises will solve.

## What to Do

### Step 1 — Download the dataset

Open Library provides free data exports at: `https://openlibrary.org/developers/dumps`

Download the **Works** export (it is a large file — be patient). It is a tab-separated file with one book per line.

Alternatively, your teacher may provide a pre-prepared CSV with 10,000 books called `books-10k.csv`.

### Step 2 — Write an import script

Write a separate script called `import_books.py` (not your main library program). This script should:
- Read the source file line by line
- Extract title, author, and year for each book
- Write the first 10,000 books to a new `library.csv`

The Open Library data is messy — some entries have missing fields, some have unusual characters. Your script will need to handle these gracefully (skip the row, or use a default value).

### Step 3 — Run the library program with 10,000 books

Start the program:
```
python library.py
```

Before the menu appears — time it. How long does it take to load?

Then try a search. Time that too.

### Step 4 — Record what you observe

Write down:
1. Time from program start to the menu appearing (use a stopwatch)
2. Time for a search to return results
3. What the experience feels like as a user

Do not fix anything yet. Just observe.

## What to Observe

With 10 books, the program felt instant. With 10,000, you will notice a pause. It may be small — or it may be large. Either way, ask yourself: what would this feel like with 100,000 books? With 1,000,000?

This is the beginning of thinking about *scale* — one of the most important concepts in engineering.

## Topics You Will Need

- File reading with `open()` and handling encoding issues (`encoding="utf-8"`)
- `try/except` to handle malformed rows
- Writing to CSV
- Understanding that reading an entire file into memory has a cost

## Before You Start — Think About This

1. When the library program starts, it reads the entire CSV into a list in memory. With 10,000 books, how much memory does that list occupy (roughly)? With 1,000,000 books, would that still work?
2. When you search for a book, the program scans every book in the list one by one. With 10,000 books, how many comparisons does one search require in the worst case?
3. The import script and the library program are two different tools. Why is it better to keep them separate rather than building the import into the main program?

## When You're Stuck

- The Open Library data uses tab characters (`\t`) as separators, not commas. Use `line.split("\t")` instead of `line.split(",")`.
- Some lines will have encoding errors. Open the file with `open(filename, "r", encoding="utf-8", errors="ignore")` to skip characters that cannot be decoded.
- If you get an `IndexError` on some lines, those lines do not have all the expected fields. Use `if len(parts) >= 3:` before trying to read fields.

## Once It Works — Go Further

1. Import 50,000 books instead of 10,000. Measure and record the startup and search times. Does performance degrade linearly (2× the data = 2× the time) or worse?
2. Use Python's `time` module to measure the startup and search times programmatically rather than with a stopwatch: `import time; start = time.time(); ...; print(time.time() - start)`.
