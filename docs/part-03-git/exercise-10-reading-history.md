---
title: "3.10 Reading History"
parent: Git & History
nav_order: 10
---

# Exercise 3.10 — Reading History

## The Story

A new engineer joins a company. She is given access to the codebase on her first day. Her task: understand why the search function behaves the way it does — specifically, why it searches by title only, not by author.

She could ask someone. But the person who made that decision left the company. She could read the code. But the code only shows *what* it does, not *why*.

She opens the git log.

Within ten minutes she finds a commit from eight months ago: *"Limit search to title only — searching by author caused performance issues with 100k+ records, to be revisited when we add an index."* The commit links to an issue with a full discussion.

She now knows more than she would have learned in an hour of asking around. The history is a record of decisions, not just changes.

**Reading git history is a skill.** Engineers who can navigate history diagnose bugs faster, understand design decisions, and avoid repeating mistakes.

## What to Do

### Part A — Navigate your own history

Run these commands on your Mini Library and answer the questions:

```
git log
```
1. How many commits do you have?
2. What does the most recent commit do?
3. What was the very first thing you committed?

```
git log --oneline
```
4. Does the one-line summary tell you enough to understand each commit?
5. Which commits have useful messages and which are vague?

```
git log --oneline --graph
```
6. Can you see where branches were created and merged?

### Part B — Find what changed and when

Use these commands to investigate specific changes:

```
git show <commit-hash>
```
This shows the full commit: message, author, date, and the diff of what changed.

```
git diff HEAD~3 HEAD
```
This shows everything that changed in the last three commits combined.

```
git log -p -- library.py
```
This shows every commit that touched `library.py`, with the full diff for each.

**Task:** Find the commit where you first added the search feature. Write down: the commit hash, the message, and one line describing what the diff shows.

### Part C — Blame

```
git blame library.py
```

`git blame` shows every line in a file, the commit that last changed it, and when. It answers: "who wrote this line, and when?"

Find the line in your library that handles CSV reading. What does `git blame` tell you about it?

(Note: despite the name, `git blame` is not about finding who to blame for a bug. It is about understanding the history of a specific line so you can read the relevant commit and understand the context.)

### Part D — The investigation exercise

Introduce a bug into your library deliberately — change the CSV reading to skip the first book in the file. Commit it with a vague message ("update"). Make two more commits of unrelated changes on top.

Now, come back after 30 minutes (or tomorrow). Using only git history tools — no re-reading the code — find the commit that introduced the bug. Write down:
1. Which command you used to find it
2. How many commits you had to look through
3. The commit hash and what the diff showed

This is what a real debugging session with Git history looks like.

## Topics You Will Learn

- `git log`, `git log --oneline`, `git log --graph` — reading history at different zoom levels
- `git show <hash>` — reading one specific commit in full
- `git diff` — comparing any two points in history
- `git log -p -- filename` — the full history of one file
- `git blame` — the history of one line in a file
- How good commit messages make history searchable

## Before You Start — Think About This

1. A commit message that says "update" tells you nothing when you are reading history. But what if the diff is simple — just one line changed? Is a vague message ever acceptable?
2. `git blame` shows who wrote each line. If you find a confusing line and `git blame` shows it was written by a colleague — what would you do next? (Hint: reading the commit message is more useful than asking the colleague immediately.)
3. The history of a project is permanent (except for the rare case of history rewriting). What does that mean for commit messages written today?

## When You're Stuck

- `git log --all --oneline --graph` shows the complete history of all branches, not just the current one.
- `git bisect` is an advanced tool for finding which commit introduced a bug using binary search — if you have a large history, look it up. It can find a bug among 1,000 commits in about 10 checks.
- If a commit hash is long, you can use just the first 7 characters — Git will find the right one.

## Once It Works — Go Further

1. Go to a popular open-source project on GitHub (try the `requests` Python library). Read the last 20 commit messages. What can you understand about the project's recent direction? What would you need to look at the code to understand?
2. Find a commit in `requests` or `flask` that has a body (a longer description below the subject line). What does the body explain that the subject could not? Why did the author write it?
