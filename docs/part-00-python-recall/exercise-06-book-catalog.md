---
title: "0.6 Book Catalog"
parent: Python Recall Bootcamp
nav_order: 6
---

# Exercise 0.6 — Book Catalog

## The Story

So far, every program you have built forgets everything the moment you close it. Member records vanish. Marks disappear. When the librarian restarts the program, they have to re-enter everything from scratch.

Real programs store data in files. This exercise teaches you to read from a file — and you will be working with a simple CSV (Comma-Separated Values) file, exactly the format the Mini Library will use.

The librarian has a file called `books.csv`. Each line has one book's details, separated by commas. Your program should read the file and display the catalog neatly.

## What to Build

First, create a file called `books.csv` in the same folder as your program. Put this in it:

```
The Alchemist,Paulo Coelho,1988
To Kill a Mockingbird,Harper Lee,1960
1984,George Orwell,1949
The Kite Runner,Khaled Hosseini,2003
Sapiens,Yuval Noah Harari,2011
```

Then write a program that reads the file and displays it like this:

```
--- Library Book Catalog ---

Title                        Author               Year
------------------------------------------------------------
The Alchemist                Paulo Coelho         1988
To Kill a Mockingbird        Harper Lee           1960
1984                         George Orwell        1949
The Kite Runner              Khaled Hosseini      2003
Sapiens                      Yuval Noah Harari    2011

Total books: 5
```

Also add a search feature:

```
Search by title (or press Enter to skip): 1984

Found: 1984 by George Orwell (1949)
```

## Topics You Will Need

- `open()` — to open a file for reading
- `for line in file:` — to go through each line
- `.strip()` — to remove the newline character at the end of each line
- `.split(",")` — to break a line into parts using the comma as the separator
- Lists — to store the parsed book data
- String formatting — to print columns that line up neatly

## Before You Start — Think About This

1. When Python reads a line from a file, it includes the newline character (`\n`) at the end. What does `.strip()` do, and why do you need it before you can use the line properly?
2. After splitting `"The Alchemist,Paulo Coelho,1988"` by comma, what do you get? How many parts are there? How do you access the title? The author? The year?
3. For the display to look neat, each column needs to take up the same width regardless of the actual content. Look up Python's string formatting with `f"{value:<30}"` — what does the `<30` mean?
4. For the search, should you read the file again, or store the books in a list while reading and search that list? Which approach is better and why?

## When You're Stuck

- The pattern to read a file safely is: `with open("books.csv", "r") as f:` — then loop through `f`. The `with` block automatically closes the file when you are done.
- After `parts = line.split(",")`, the title is `parts[0]`, the author is `parts[1]`, and the year is `parts[2]`.
- To make columns align, try: `f"{title:<30}{author:<22}{year}"` — the number is the total width for that column, and `<` means left-aligned.
- If the file does not exist, Python will throw an error. Look up how to handle this with a `try/except` block.

## Once It Works — Go Further

1. Sort the catalog alphabetically by title before displaying it. Look up Python's `sorted()` function.
2. Add a filter — ask whether to show books before or after a certain year, then display only those.
3. Count how many books each author has and print a summary: `Paulo Coelho: 1 book`, etc.
