---
title: "4.3 Split into Modules"
parent: Refactoring
nav_order: 3
---

# Exercise 4.3 — Split into Modules

## The Story

The librarian calls again: "We are switching from CSV files to a proper database. Can you update the program?"

You open `library.py`. The functions that handle CSV reading and writing are there — but so is the menu code, the search code, the display code. The CSV logic is mixed in with everything else. To change the storage format, you have to read through menu logic and display logic to find the relevant lines. You change one function and accidentally break a display function that was three lines away.

This is what it means for concerns to be mixed: *changing one thing requires understanding everything*.

Now imagine a different design: one file handles storage, one file handles book logic, one file handles the interface. The librarian asks you to change storage. You open `storage.py`. Everything you need is there. You make the changes. You do not touch `books.py` or `interface.py` — they do not know or care how storage works.

This property — changing one thing without touching the rest — is called **separation of concerns**. It is one of the most important ideas in software design.

## What to Do

### Part A — Name the three concerns in your library

Before creating any files, identify the three (or more) distinct concerns in your current codebase. For each concern, write:

- A one-word name for it
- A description in one sentence: "This concern handles..."
- The names of the functions currently in `library.py` that belong to it

You should find at least three concerns. Common ones: storage (reading/writing files), book logic (searching, validating, adding), interface (menus, input, display). You might find more.

If a function belongs to two concerns, that is a signal — which concern does it *primarily* belong to, and what is it doing that it should not?

### Part B — Draw the dependency diagram

Before moving any code, draw which module will depend on which.

For example: does the interface need to call storage functions directly? Or does it call book functions which call storage? Which module is at the centre — the one that knows nothing about the others?

Draw this on paper. Arrow means "depends on" or "calls functions from."

The goal is to have no circular dependencies — A depends on B, but B never depends on A. If you find a circle, you need to rethink your module boundaries before moving any code.

### Part C — Move one function at a time

Create your new module files. Move one function into the correct file. Then immediately run the program — everything must still work. Update any imports in `library.py` to use the new location.

Move the next function. Run the program again.

Do not move five functions and then try to fix all the errors. That approach makes it impossible to know which move caused a problem.

### Part D — Change the storage format

Once the split is complete, test the core promise: the librarian asks you to change the CSV column order — `title,author,year` becomes `year,title,author`. Make this change.

How many files did you have to touch?

Before the split, the answer was "I had to read the whole thing." After the split, the answer should be "only the storage module."

If you had to touch more than one module to change the storage format, your module boundaries were not clean enough. Investigate why — what leaked out of the storage module into the others?

## Before You Start — Think About This

1. Two modules that depend on each other (circular dependency) cannot be tested or changed independently. If `books.py` imports from `storage.py` AND `storage.py` imports from `books.py` — what happens when you try to load either one? Why does Python struggle with this?
2. A well-designed module hides its implementation. If `interface.py` knows that books are stored in a CSV (and uses that knowledge directly), what happens when you switch to a database? What should `interface.py` know about storage?
3. One sign of a good module split: you can describe what each module does in one noun. "Storage handles persistence." "Books handles the collection." "Interface handles the user." If you cannot describe a module in one noun, it is probably doing too many things.

## When You're Stuck

- The `import` statement in Python lets one file use functions from another. You do not need any new syntax — just `import` what you need.
- Circular imports cause an error at startup. If you get one, trace the dependency chain — which module is depending on something it should not need?
- If you discover that a function needs data from a module it should not know about, that data should probably be passed as a parameter instead of imported.

## Once It Works — Go Further

1. Add a `config.py` containing only constants: the filename, the CSV column order, any other fixed values. Import these constants into the modules that need them. What is the benefit of having all constants in one place?
2. Now count the lines in each module. If one is much longer than the others, ask why — is it doing more than its share? What would you split out of it?
