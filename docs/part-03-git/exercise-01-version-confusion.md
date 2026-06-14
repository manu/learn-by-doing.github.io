---
title: "3.1 Version Confusion"
parent: Git and History
nav_order: 1
---

# Exercise 3.1 — Version Confusion

## The Story

You have been working on the Mini Library for two weeks. Every time you make a change you are not sure about, you save a copy:

```
mini-library/
    library.py
    library_v2.py
    library_backup.py
    library_final.py
    library_final2.py
    library_final_FIXED.py
    library_final_latest.py
    library_final_latest_REAL.py
```

It is now Tuesday afternoon. You discover a bug introduced three days ago. You need to go back to the version from last Friday — the one that was working — and start from there.

Which file is that?

You open each one. Some look similar. Some have features that others don't. The timestamps are unreliable — some files were copied, so their "modified" date is today. The filenames tell you nothing useful. "Final" is a lie. "Latest" appears four times.

You spend 45 minutes. You are not confident you found the right one.

## What to Do

### Part A — Recreate the problem

Build this folder structure for real. Take your current `library.py` and make copies:

```
library.py           ← the real current file
library_v2.py        ← copy of library.py, but remove the search feature
library_backup.py    ← copy with a deliberate bug (print the wrong total count)
library_final.py     ← copy with a feature added (show book count in menu)
library_FIXED.py     ← copy with library_backup's bug "fixed" but search still missing
```

Now close all the files. Come back after 10 minutes and try to answer:

1. Which version has both search AND the correct total count?
2. Which version is the most recent?
3. Which version has all features working correctly?

Write down how you figured it out. How long did it take? What information was missing?

### Part B — Write down the pain

Answer these questions honestly:

1. What would you need to add to each filename to make the version instantly clear?
2. What information does a filename *cannot* carry, no matter how long you make it?
3. If two people had been working on these files at the same time — one adding the search feature, the other fixing the bug — what would have happened to the files?
4. What would a perfect version-tracking system do that filenames cannot?

Write at least one sentence for each answer. This is your requirement list for the tool you are about to learn.

### Part C — The question that Git answers

Before learning any Git commands, write down five questions you would want a version-tracking system to answer:

1. What changed between the version from last Friday and today?
2. Who changed it?
3. Why was this change made?
4. Can I go back to any past version without losing the current one?
5. (Your own question)

Keep this list. After learning Git, come back and check whether Git answers all of them.

## Topics You Will Learn

- Why file-copy version control fails at scale
- What information a version control system must track (what, who, when, why)
- The concept of a complete, ordered history
- Why Git was invented and what problem it was designed to solve

## Before You Start — Think About This

1. The file `library_final_latest_REAL.py` exists. What does this filename tell you about the person who created it? What were they feeling when they named it?
2. A musician makes a recording, calls it "track_final_v3_MASTER_mixdown_fixed.mp3". What does this tell you about the tools they are using? What tools do professional recording studios use instead?
3. If ten engineers are working on the same project at the same time and each one keeps their own copies — how many copies exist? How do you combine their changes?

## When You're Stuck

- For Part A, you do not need real feature differences — just change one visible thing in each copy (a print message, a variable name) so you can tell them apart.
- The point of Part B is to feel the problem, not to solve it. Write down what is frustrating. That frustration is the best motivation for learning Git.

## Once It Works — Go Further

1. After completing this exercise, search for the story of why Linus Torvalds created Git in 2005. What was the specific problem he was trying to solve? How does it relate to the problem you just experienced?
2. Before Git, engineers used other version control tools (CVS, SVN, Perforce). Look up one of them. What could it do that the file-copy approach could not? What could Git do that they could not?
