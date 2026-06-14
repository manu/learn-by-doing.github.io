---
title: "1.4 Comment the Why"
parent: Engineering Mindset
nav_order: 4
---

# Exercise 1.4 — Comment the Why, Not the What

## The Story

A junior engineer once wrote this comment in a large production codebase:

```python
# add 1 to count
count = count + 1
```

This comment tells you nothing you could not already see. The code says the same thing. A comment that restates the code wastes the reader's time.

A year later, a bug appeared. Someone removed that `count = count + 1` line, thinking it was redundant. The entire system started miscounting book checkouts. The bug took three days to find.

If the comment had said:

```python
# reservation count includes holds, not just current loans — matches librarian contract
count = count + 1
```

…nobody would have touched it.

The difference: one comment tells you *what*. The other tells you *why*.

## What to Do

### Part A — Identify the useless comments

Here are several comments. Your task is to label each one:
- **Useless** — it restates what the code already says
- **Useful** — it explains a decision, a constraint, or a surprise

Think about why each one is useful or useless:

```
# loop through books
for book in books:

# check if year is after 1900 because our library database starts from 1901
if year > 1900:

# return None
return None

# using linear search here because binary search requires a sorted list
# and sorting 10k books on every search is too slow
for book in books:
    if book["title"] == query:
        return book

# multiply by 100
percentage = (found / total) * 100

# CSV has no header row — first import from the school system stripped it
reader = csv.reader(file)
```

Write a one-sentence explanation for why each comment is or isn't useful.

### Part B — Fix the useless comments in your Mini Library

Open your `library.py`. Look for any comments you have written. For each one:

1. Does this comment tell me something the code doesn't already show?
2. Does this explain *why* a decision was made, not just *what* the code does?

Remove every comment that fails. Rewrite any comment that *could* be useful but is currently explaining what instead of why.

### Part C — Find the uncommented decisions

Now look for places in your Mini Library where you made a non-obvious decision and left no comment. A few questions to guide you:

- Why did you choose to store books as a list of dictionaries, not a list of lists?
- Why does your search function compare lowercase versions of strings?
- If your CSV has a specific column order — why that order?

For each non-obvious decision, write one comment explaining the choice. If you cannot remember why you made the decision, that itself is a problem worth noting.

## Topics You Will Learn

- The difference between comments that explain *what* (useless) and *what* (useful)
- When to comment and when to let the code speak for itself
- Why well-named code often needs no comments at all
- How comments age badly when code changes but comments don't

## Before You Start — Think About This

1. If you rename a variable to something more descriptive, do you still need a comment explaining what it is? Give an example.
2. Comments can lie. If you change the code but forget to update the comment, the comment now says something false. What does this tell you about how many comments to write?
3. Some engineers say: "If your code needs comments, your code is not clear enough." Others say: "Even perfect code cannot explain *why* a decision was made." Who is right?

## When You're Stuck

- Ask yourself: "If I erased this comment, would a future reader lose any information?" If no — delete it.
- A useful comment often starts with: "because", "this handles", "we do this instead of", "the reason", "note that".
- If you're writing a comment that starts with "this function does X" — that belongs in the function name, not a comment.

## Once It Works — Go Further

1. Look at a real open-source Python project on GitHub — try `requests` (the HTTP library). Find three comments in the source code. For each, decide: is it a what-comment or a why-comment? Would you keep it or delete it?
2. Write a short rule for yourself: "I will write a comment when \_\_\_\_\_ and not write one when \_\_\_\_\_." Keep this rule in your engineering notes.
