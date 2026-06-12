---
title: "3.3 Branches"
parent: "Git & History"
nav_order: 3
---

# Exercise 3.3 — Branches

## The Story

The Mini Library is working. A user has asked for a new feature: the ability to mark a book as "borrowed" and track who borrowed it.

The problem: adding this feature will require changes to several parts of the program. If you make those changes directly on the working version and something breaks halfway through, you are stuck with a broken program and no way to go back to the version that was working.

Branches solve this. A branch is a parallel copy of the history where you can experiment freely. If the experiment works, you merge it back. If it does not, you discard it — the original is untouched.

## What to Do

### Step 1 — Create a branch for the new feature

```
git branch feature-borrow-tracking
git checkout feature-borrow-tracking
```

Or in one step:
```
git checkout -b feature-borrow-tracking
```

Run `git branch` to confirm you are now on the new branch.

### Step 2 — Build the feature

On this branch, add a "borrow" feature to the library:
- Add a `borrowed_by` field to each book (empty by default)
- Add a menu option: `5. Borrow a book`
- The user types the title and their name — the book is marked as borrowed
- When listing books, show who has borrowed each book (or "Available" if nobody has)

Commit your changes on this branch as you go. Aim for at least two commits: one for the data change, one for the menu logic.

### Step 3 — Check that main is unchanged

```
git checkout main
python library.py
```

The main branch should run exactly as it did before your feature work. The feature does not exist here yet.

### Step 4 — Merge the branch

Once the feature is complete and working:

```
git checkout main
git merge feature-borrow-tracking
```

Now run the program from main — the feature is there.

### Step 5 — Delete the branch

```
git branch -d feature-borrow-tracking
```

The branch has served its purpose. Its commits are now part of the main history.

## What to Observe

Run `git log --oneline` on main after the merge. You will see all the commits from both the main branch and the feature branch, in chronological order. This is the value of branches: parallel work with a clean merge point.

## Topics You Will Learn

- `git branch`, `git checkout`, `git merge`
- The concept of HEAD (which branch/commit you are currently on)
- Why branches enable safe experimentation
- What a merge means and what a merge conflict is (and how to resolve one)

## Before You Start — Think About This

1. Without branches, what would you do to work on a risky new feature without risking the working version? What problems does that approach have?
2. If two people are working on the same project at the same time — one on a search feature, one on a borrow feature — how do branches help them work independently?
3. What do you think happens if both branches change the same line of code? How would Git know which version to keep?

## When You're Stuck

- `git branch` with no arguments lists all branches. The one with `*` is your current branch.
- If a merge fails with a conflict, Git marks the conflict in the file with `<<<<`, `====`, and `>>>>` markers. Open the file, choose which version you want, remove the markers, then `git add` and `git commit` to complete the merge.
- `git log --oneline --graph` draws an ASCII diagram of the branch history — useful for visualising what happened.

## Once It Works — Go Further

1. Create a second branch called `bugfix-search-case` and fix the search so it is case-insensitive (if it is not already). Merge it into main separately from the feature branch. Look at the commit history — notice how each concern has its own clean commit trail.
2. Look up what `git stash` does. Try using it to save unfinished work temporarily before switching branches.
