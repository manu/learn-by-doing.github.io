---
title: "3.7 Merge Conflicts"
parent: Git and History
nav_order: 7
---

# Exercise 7.7 — Merge Conflicts

## The Story

Two engineers are working on the Mini Library at the same time:

- Engineer A is on branch `feature-search`: she changes the search function to be case-insensitive
- Engineer B is on branch `feature-delete`: he adds a delete feature, and as part of that work, also changes the search function to log all searches to a file

Both branches change the same function. When Engineer B's branch is merged first, and then Engineer A tries to merge hers — Git cannot decide which version of the search function to keep.

This is a **merge conflict**. Git is not broken. Git is not failing. Git is doing exactly what it should: it has found a place where two humans made different decisions and it is asking a human to resolve the disagreement.

Merge conflicts are a normal part of working with Git. Every engineer encounters them. The skill is not avoiding them — it is resolving them calmly and correctly.

## What to Do

### Part A — Create a conflict deliberately

Set up a situation that will produce a conflict:

1. On `main`, you have this in your library:
   ```
   def display_books(books):
       print("=== All Books ===")
       for book in books:
           print(book["title"])
   ```

2. Create branch `feature-a`:
   ```
   git checkout -b feature-a
   ```
   Change `display_books` to show the author as well: `print(book["title"], "-", book["author"])`
   Commit the change.

3. Go back to main. Create branch `feature-b`:
   ```
   git checkout main
   git checkout -b feature-b
   ```
   Change the same `display_books` function to add a book count header: `print(f"=== All Books ({len(books)}) ===")`
   Commit the change.

4. Merge `feature-a` into main:
   ```
   git checkout main
   git merge feature-a
   ```
   This will succeed — main has no conflicting changes.

5. Now merge `feature-b`:
   ```
   git merge feature-b
   ```
   Git will report a conflict.

### Part B — Read the conflict markers

Open the conflicting file. You will see something like this:

```
<<<<<<< HEAD
def display_books(books):
    print("=== All Books ===")
    for book in books:
        print(book["title"], "-", book["author"])
=======
def display_books(books):
    print(f"=== All Books ({len(books)}) ===")
    for book in books:
        print(book["title"])
>>>>>>> feature-b
```

Understand each part:
- Everything between `<<<<<<<` and `=======` is what the current branch (HEAD/main) has
- Everything between `=======` and `>>>>>>>` is what the incoming branch (feature-b) has
- Git is asking you to decide: keep one, keep the other, or combine them

### Part C — Resolve the conflict

The correct resolution is to keep BOTH changes — show the count in the header AND show the author in each row. Edit the file to achieve this, removing all the conflict markers. Then:

```
git add library.py
git commit -m "Merge feature-b: combine count header with author display"
```

Run the program and verify it works.

### Part D — Understand the principles of conflict resolution

Answer these questions after resolving:

1. Who should resolve a conflict — the person who wrote the incoming branch, the person who maintains main, or someone else?
2. After resolving, you must test the program manually. Why? What could go wrong in a conflict resolution even if you removed the markers correctly?
3. If Engineer A and Engineer B were working in the same room, how would the conflict resolution conversation go?

## Topics You Will Learn

- What a merge conflict is and why it happens
- How to read `<<<<<<<`, `=======`, `>>>>>>>` markers
- How to resolve a conflict by choosing, discarding, or combining changes
- `git add` and `git commit` to complete a conflict resolution
- Why testing after resolution is essential

## Before You Start — Think About This

1. Git tracks lines, not meaning. If two branches change the same *line* in different ways, Git flags it as a conflict — even if the changes are logically compatible. What does this tell you about how to design commits to minimise conflicts?
2. A conflict only happens when two branches change the *same part* of the same file. If Engineer A changes the search function and Engineer B changes the add function in the same file — does a conflict happen?
3. Some teams have a rule: "Keep feature branches short-lived." If a feature branch exists for only one or two days, are conflicts more or less likely? Why?

## When You're Stuck

- `git status` after a failed merge shows which files have conflicts — look for "both modified".
- `git merge --abort` cancels the merge entirely and returns you to where you were before. Use this if you need to stop and think.
- `git log --oneline --graph --all` draws the branch history visually — useful for understanding what happened before the conflict.
- Every conflict marker line (`<<<<<<<`, `=======`, `>>>>>>>`) must be removed before the file is valid Python. If you accidentally leave one in, the program will crash with a `SyntaxError`.

## Once It Works — Go Further

1. Create a conflict in the CSV reading code. Resolve it in a way that combines both changes. Practice until resolving a conflict takes less than 5 minutes — that is the real skill benchmark.
2. Look up what `git rerere` does. If you work on a long-running branch that frequently needs to merge from main, `rerere` can remember how you resolved a conflict and apply it automatically next time.
