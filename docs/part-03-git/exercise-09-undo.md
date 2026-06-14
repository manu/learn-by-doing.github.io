---
title: "3.9 Undoing Mistakes"
parent: Git & History
nav_order: 9
---

# Exercise 3.9 — Undoing Mistakes

## The Story

It is 11pm. You have been working on the library for two hours. You made a change that seemed good, committed it, made three more commits on top, and now the program is completely broken in a way you do not understand.

You want to go back. But how? There are four different levels of "oops" in Git, each requiring a different command. Using the wrong one can make things worse.

Knowing how to undo in Git is the skill that makes you fearless. When you know you can always go back, you experiment more freely. When you don't know — you are afraid to commit, afraid to branch, afraid to try things. That fear makes you a worse engineer.

## The Four Levels of Undo

Study these before touching any commands:

**Level 1 — Unstaged change** (you edited a file but have not run `git add`)
You just want to throw away an edit to a file.
```
git restore filename.py
```

**Level 2 — Staged change** (you ran `git add` but have not committed yet)
You staged the wrong file. Put it back to unstaged.
```
git restore --staged filename.py
```

**Level 3 — Last commit** (you committed but have not pushed)
The commit is wrong and you want to redo it. This rewrites history — only safe before pushing.
```
git commit --amend
```
Or to undo the commit entirely but keep the changes as unstaged edits:
```
git reset HEAD~1
```

**Level 4 — A pushed commit** (others may have it already)
You cannot rewrite history. Instead, create a new commit that undoes the old one.
```
git revert <commit-hash>
```

## What to Do

### Part A — Practice each level

Set up each situation in your Mini Library and practice the correct undo:

**Scenario 1:** Edit `library.py` to add a bad print statement. Do NOT add or commit. Undo the edit and verify the file is back to its previous state.

**Scenario 2:** Edit `library.py`, run `git add library.py`. Then realise you do not want to stage it yet. Unstage it, without losing the edit.

**Scenario 3:** Make a small commit with a typo in the commit message. Correct the message using `--amend` before pushing.

**Scenario 4:** Commit a change that removes the search feature accidentally. Create a new commit that reverses that specific commit using `git revert`.

### Part B — Understanding git reset depth

`git reset` has three modes. Study each and describe in your own words what each one does:

- `git reset --soft HEAD~1` — undoes the commit but keeps everything staged
- `git reset HEAD~1` (same as `--mixed`) — undoes the commit and unstages, but keeps file changes
- `git reset --hard HEAD~1` — undoes the commit AND discards all file changes

Which one is dangerous and irreversible? When would you use each?

### Part C — The golden rule of rewriting history

There is one rule in Git that, if broken, causes serious problems for everyone on a team:

**Never rewrite history that has already been pushed.**

`git commit --amend` and `git reset` rewrite history. If you have already pushed those commits and someone else has pulled them, you will create a diverged history that is very painful to reconcile.

`git revert` is always safe because it adds a new commit rather than changing the past.

Write one rule that describes when to use `reset/amend` and when to use `revert`. Keep it in your Git notes.

## Topics You Will Learn

- `git restore` — undo changes to a file (before staging)
- `git restore --staged` — unstage a file
- `git commit --amend` — fix the last commit (before pushing only)
- `git reset HEAD~1` — undo the last commit, keep changes
- `git reset --hard` — undo commit AND discard changes (dangerous)
- `git revert` — safely undo a pushed commit by adding a new commit
- The golden rule: never rewrite pushed history

## Before You Start — Think About This

1. Why is `git reset --hard` dangerous? What does it do that cannot be easily undone?
2. `git revert` creates a new commit that undoes a previous one. The original bad commit still exists in history. Is that a problem? Why might it actually be useful?
3. A colleague tells you: "I never commit until I'm certain the code is perfect — I'm too afraid of getting into a mess." What would you tell them about how Git undo works?

## When You're Stuck

- If you are not sure which level of undo you need, run `git status` first. It tells you exactly the state of each file.
- `git log --oneline` shows the recent history so you can find the commit hash you need for `git revert`.
- `git reflog` is an emergency tool — it shows every action Git has taken, including things `git log` does not show. If you use `git reset --hard` and lose work, `git reflog` can help you find it.

## Once It Works — Go Further

1. Look up `git reflog`. Run it on your repository. What does it show? How is it different from `git log`? Why is it the "emergency recovery" tool?
2. Try this: make a change, commit it, then use `git reset --hard HEAD~1` to discard it. Then use `git reflog` to find the discarded commit and recover it with `git checkout <hash>`. This technique has saved many engineers from disaster.
