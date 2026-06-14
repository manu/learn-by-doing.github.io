---
title: "3.2 First Commit"
parent: Git and History
nav_order: 2
---

# Exercise 3.2 — First Commit

## The Story

After the Version Confusion exercise, you felt the problem: without a history tool, you cannot tell which file is the real one, who changed it, or why.

Git solves this by recording every change as a *commit* — a snapshot of the project at a specific moment, with a message explaining what changed and why. Unlike a filename like `library_FINAL2.py`, a commit message is part of a permanent, ordered history.

This exercise gets your Mini Library into Git for the first time.

## What to Do

### Step 1 — Initialise the repository

Navigate to your Mini Library folder in the terminal. Then initialise a Git repository:

```
git init
```

Git will tell you a repository has been created. Nothing has been saved yet — you have only created an empty history.

### Step 2 — Check the status

```
git status
```

Git will show you every file in the folder that it is not yet tracking. These are *untracked* files.

### Step 3 — Stage your files

Tell Git which files to include in the first commit:

```
git add library.py
git add README.md
```

Do not add `library.csv` — data files do not belong in version control. Run `git status` again and observe the difference.

### Step 4 — Write your first commit message

```
git commit -m "Add Mini Library — menu-driven book manager with CSV storage"
```

Read the message before pressing Enter. Ask yourself: if you found this commit in the history six months from now, would it tell you what the program does?

### Step 5 — View the history

```
git log
```

You will see your first commit: its unique ID (the hash), your name, the date, and your message.

### Step 6 — Make a change and commit again

Add one feature to your library (for example: show the total number of books at the top of the list view). Then commit that change with a message that describes *what changed and why* — not just "update" or "fix".

## What to Observe

After two commits, run `git log` and `git diff HEAD~1` (compare the latest commit with the previous one). You should be able to see exactly what line changed between commits.

This is what was missing from the folder full of `library_FINAL2.py` files.

## Topics You Will Learn

- `git init`, `git add`, `git status`, `git commit`, `git log`
- The difference between *staging* (what goes into the next commit) and *committing* (saving the snapshot)
- What a commit hash is
- Why `.csv` and other data/generated files do not belong in version control

## Before You Start — Think About This

1. A commit message like `"changes"` is technically valid — Git will accept it. Why is it a bad commit message? What makes a commit message useful?
2. Git tracks files, not folders. If you have an empty folder, Git ignores it. Why do you think this design decision was made?
3. `git add` stages a file, but `git commit` saves it. Why are these two separate steps instead of one?

## When You're Stuck

- If `git commit` opens a text editor unexpectedly, you can exit by typing `:q` and pressing Enter (in vim) or by closing the window. Use `-m "message"` to avoid this.
- If you accidentally add the wrong file, use `git restore --staged filename` to unstage it before committing.
- `git log --oneline` gives a compact one-line view of each commit — useful when history gets long.

## Once It Works — Go Further

1. Create a `.gitignore` file that tells Git to ignore `library.csv` automatically. Look up the `.gitignore` format. Test it by running `git status` after adding the file.
2. Make three more small commits — each one a tiny change with a descriptive message. Then run `git log --oneline` and read the history as if you were someone who had never seen this project. Does it tell a coherent story?
