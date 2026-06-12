---
title: "4.2 Extract Functions"
parent: Refactoring
nav_order: 2
---

# Exercise 4.2 — Extract Functions

## The Story

After Exercise 4.1, you identified sections of the library code that are doing too many things at once. The main loop handles input, validates it, performs the action, and formats the output — all in one place. This makes it impossible to test any individual part, and very hard to change one behaviour without affecting another.

The most important refactoring technique is *extract function*: taking a named chunk of logic out of a large block and giving it its own function. This is not just about making the file shorter — it is about giving ideas names.

## What to Do

### Step 1 — Find the sections that have no names

Look at your main loop. It probably contains inline code for:
- Displaying the menu
- Reading and validating user input
- Loading books from the CSV
- Saving a book to the CSV
- Searching for a book
- Printing the book list

These are *concepts* in your program that currently have no names. They are just blocks of code sitting inside a loop.

### Step 2 — Extract each concept into a function

For each concept, do this one at a time:
1. Write a function with a clear name: `show_menu()`, `load_books()`, `save_book(book)`, `search_books(books, query)`, `print_book_list(books)`
2. Move the relevant code into the function
3. Call the function from where the code used to be
4. Run the program — behaviour must be identical

### Step 3 — Read the main loop after extraction

When the extractions are complete, your main loop should read almost like English:

```
books = load_books()
while True:
    show_menu()
    choice = get_user_choice()
    if choice == "1":
        book = get_book_details()
        books.append(book)
        save_book(book)
    elif choice == "2":
        print_book_list(books)
    ...
```

If you can read the main loop and understand the program's behaviour without needing to read any function bodies, the extraction is working.

### Step 4 — Verify the single responsibility

For each function you extracted, ask: does this function do *one thing*? If a function loads books AND validates their format AND prints an error — it is doing three things. Split it further.

## Topics You Will Learn

- Extract function — how and when to apply it
- Single responsibility: each function should do one thing and name it
- How extracted functions make testing possible (you can test each one in isolation)
- The relationship between function names and code readability

## Before You Start — Think About This

1. What is "one thing"? A function that loads a CSV file is doing one thing. A function that loads a CSV file AND checks for duplicates AND sorts the result — how many things is that?
2. After extraction, the total number of lines in the file might actually *increase* (due to function definitions, blank lines, etc.). Is that a problem? Why or why not?
3. A function with parameters is more flexible than one that reads global variables. How does extraction naturally lead you away from globals?

## When You're Stuck

- Start with the easiest extraction: `show_menu()`. It is a pure output function with no logic. Extract it, verify the program still works, then move on to harder extractions.
- If a function needs data that is currently in the global scope, make that data a parameter. Ask: what does this function need to know to do its job?
- If a function produces data that the caller needs, it should return that data. Ask: what does this function produce?

## Once It Works — Go Further

1. Write a short test for `search_books(books, query)`. Call it directly with a known list of books and a known query, and verify the result without running the whole program. This is your first taste of unit testing.
2. Extract one more function that you did not plan for — one that emerges naturally from reading the code after the first round of extractions. Often, refactoring reveals abstractions that were not visible before.
