---
title: "3.6 Commit Messages"
parent: Git and History
nav_order: 6
---

# Exercise 3.6 — The Art of the Commit Message

## The Story

Here is the git log of a real project:

```
a3f8c12  fix
b91d044  update
c23e711  changes
d004a1f  more changes
e8ab321  fixed it
f19c230  final fix
g923b11  actually final fix
h001c22  ok this is the real fix
```

Eight commits. Zero information.

If you were asked to find the commit that introduced the bug causing the wrong book count, where would you start? You would have to open each one, read the diff, and guess.

Now look at this log from a different project:

```
a3f8c12  Fix book count off-by-one when CSV has trailing newline
b91d044  Add case-insensitive search to fix "sapiens" not finding "Sapiens"
c23e711  Refactor: extract CSV reading into load_books() for reuse
d004a1f  Add delete-by-title feature (closes #12)
e8ab321  Validate year input — reject non-numeric values gracefully
```

Five commits. You can read the history like a story. You can find the exact commit that changed book counting in three seconds.

The commit message is a letter to the future. You are writing it for yourself six months from now, for a colleague who joins the project next year, for whoever has to fix the bug that your code will inevitably contain.

## What to Do

### Part A — Grade the bad messages

For each commit message below, write:
- Why it fails (what it does not tell you)
- A rewritten version that would be genuinely useful

```
1. "fix"
2. "update library.py"
3. "added stuff"
4. "oops"
5. "working now"
6. "WIP"
7. "temp"
8. "it works!!!"
```

### Part B — Learn the structure

A good commit message has two parts:

**Subject line** (first line): What changed, in 50–72 characters. Written as a command: "Fix", "Add", "Remove", "Update", "Refactor", not "Fixed", "Adding", "I updated".

**Body** (optional, after a blank line): Why the change was made. What problem it solves. What approach was chosen and why. Not a description of what the diff shows — anyone can read the diff.

Example:
```
Fix book count off-by-one when CSV has trailing newline

The CSV reader was counting blank lines as books. Added a check to skip
lines where title is empty. Discovered during testing with a 10,000-book
dataset exported from Open Library.
```

### Part C — Audit your own history

Run `git log --oneline` on your Mini Library. Read every commit message you have written. For each one:
- Does it tell you what changed?
- Does it tell you why?
- Could you use it to find a specific change three months from now?

Rewrite the worst three. You cannot change the past commits (that would rewrite history others might depend on), but you can write better ones going forward. Write your three rewrites as if they were going into the log today.

### Part D — Your personal commit message rules

Write three to five rules you will follow for every commit message from now on. Base them on what you learned in Parts A–C.

Keep this list in your README or in a file called `CONTRIBUTING.md`. These rules are your engineering standard.

## Topics You Will Learn

- What makes a commit message useful vs useless
- The subject line / body structure
- Imperative mood: "Fix", not "Fixed" or "Fixing"
- Why the message explains *why*, not *what* (the diff shows what)
- How commit history becomes a searchable, readable record of decisions

## Before You Start — Think About This

1. A commit message says "fix bug." Six months later, there is a regression. You search the history to understand when the bug was introduced and what fixed it. How useful is "fix bug"?
2. The subject line should be 50–72 characters. Why might there be a character limit? What does it force you to do?
3. If you were reading a pull request on GitHub, would you read the commit messages? When would they matter more than the PR description?

## When You're Stuck

- If you struggle to write the subject line, you might be committing too many changes at once. One commit should do one thing — then describing it is easy.
- Start with the verb: "Add", "Fix", "Remove", "Update", "Refactor", "Move", "Rename", "Test". Picking the right verb forces clarity about what kind of change this is.
- The test: if you showed only the subject line to someone who knows the project, would they know what changed without looking at the diff?

## Once It Works — Go Further

1. Look up the "seven rules of a great Git commit message" (a famous blog post by Chris Beams). Compare his rules with yours — where do they agree? Where do they differ?
2. Many open-source projects have a `CONTRIBUTING.md` file that specifies exactly how commit messages must be formatted. Find one (try the Linux kernel or Angular). What rules do they enforce? Why would a large team need formal rules that a solo developer might not?
