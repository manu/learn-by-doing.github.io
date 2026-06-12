---
title: "1.2 Bad Variable Names"
parent: Engineering Mindset
nav_order: 2
---

# Exercise 1.2 — Bad Variable Names

## The Story

Here is a function from a real project. Can you tell what it does?

```python
def proc(d, x, y):
    r = []
    for i in d:
        if i[x] > y:
            r.append(i)
    return r
```

It works perfectly. It passes all its tests. A senior engineer wrote it.

And yet — if you come back to this code three weeks later, you will spend ten minutes figuring out what `d`, `x`, `y`, `r`, and `i` mean. Multiply that by thousands of functions across a large project, and you have a system that nobody can safely change.

Naming is not a style preference. It is how engineers communicate with each other — and with their future selves.

## What to Do

### Part A — Rename the mystery function

Study the function above. Figure out what it does (you may need to trace through it with a small example). Then rewrite it with names that make its purpose obvious. Do not change a single line of logic — only change the names.

After your rename, someone should be able to read the function and understand it without running it.

### Part B — Audit the Mini Library

Open your `library.py` from Part 0. Go through every variable, function, and parameter name. For each one, ask:

- Does this name tell me what the thing *is* or what it *holds*?
- Would a person who has never seen this code understand it immediately?
- Is this name accurate? (A variable named `books` that sometimes holds members is worse than a variable with a bad name — it actively misleads.)

Make a list of every name that fails these questions. Then rename them.

### Part C — The naming rules to remember

After completing Parts A and B, write down your own naming guidelines — three to five rules you will follow from now on. Base them on what you discovered, not on what you read somewhere.

## Topics You Will Learn

- Variable naming conventions in Python (`snake_case`)
- The difference between names that describe *what something is* versus *what it does*
- Why short names (`x`, `i`, `tmp`) are acceptable inside tiny loops but dangerous in larger scope
- How naming is a form of documentation

## Before You Start — Think About This

1. What is the difference between `d` and `data` and `filtered_books`? All three could refer to the same value. Which one helps you the most, and why?
2. Is `get_books()` a good function name? What about `load()`? What about `load_books_from_csv()`? At what point does a name become too long?
3. Single-letter variable names like `i` in a `for i in range(10):` loop are considered acceptable by most engineers. Why do you think that exception exists?

## When You're Stuck

- If you cannot think of a good name, describe in a sentence what the variable holds. Then use the key noun from that sentence as the name.
- A function name should usually be a verb + noun: `add_book`, `search_members`, `calculate_average`. If you cannot describe a function with a verb+noun, the function might be doing too many things.
- Read the code out loud as if explaining it to someone. Where you feel the need to say "this is the..." — that gap is a naming problem.

## Once It Works — Go Further

1. Look at the Python standard library — open `os.path` or `datetime` in your Python installation and read the source. Are the names there good? Are there any that surprise you?
2. Find one example in your Mini Library where a better name would have prevented a bug or a misunderstanding. Write one sentence explaining what the name was, what it should have been, and what confusion it caused.
