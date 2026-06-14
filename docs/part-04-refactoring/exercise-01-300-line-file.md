---
title: "4.1 The 300-Line File"
parent: Refactoring
nav_order: 1
---

# Exercise 4.1 — The 300-Line File

## The Story

The Mini Library started as 50 lines. Then you added borrow tracking. Then delete. Then case-insensitive search. Then input validation. Then a count display. Each addition was small and reasonable. Each time, you added to the file.

It is now 300 lines. It still works perfectly.

One morning the librarian calls: "I need one more thing — when listing books, I want to see which ones are overdue." You open `library.py`. You start reading. Ten minutes later you are still reading — trying to understand what interacts with what before you dare change anything. You are afraid that touching one part will break another.

This feeling has a name: **technical debt**. The code is not broken. It is *fragile* — any change risks something unexpected. The debt accumulated invisibly, one small addition at a time.

The way to pay it back is refactoring.

## What to Do

### Part A — Attempt the change first

Before reading or reorganising anything, try to add the overdue feature directly. Spend 20 minutes trying to work out where to add it and what it would affect.

Write down:
1. How many places in the file did you have to read before you understood enough to start?
2. Were you confident that your change would not break anything else?
3. Did you actually finish the feature, or did the complexity stop you?

This is the pain. Keep this record — you will compare it to the same task after refactoring.

### Part B — Diagnose before you touch

Now read the entire file from top to bottom. Do not change anything. As you read, make a written list:

- Every place where you thought "what does this do?" and had to re-read it
- Every function that does more than one thing (search AND display, load AND validate)
- Every variable name that could mean more than one thing
- Every piece of logic that appears more than once
- Every section where a comment explains *what* the code does — this is almost always a sign the code could explain itself through better naming

This is your diagnosis. A doctor diagnoses before prescribing.

### Part C — Choose one thing and fix it

From your diagnosis, pick the single most confusing section — not the biggest, the most *contained* one. The one you feel most certain about.

Fix only that one thing. Then run the program and verify it behaves identically to before. Every feature must still work.

Write down: what you changed, why, and how you verified nothing broke.

### Part D — Reflect on the process

After one change:
1. Did fixing that one section make nearby code easier to read?
2. Did it reveal another problem that was hidden before?
3. Were you tempted to fix multiple things at once? What would have happened if you had?

Refactoring is not a one-time cleanup. It is a discipline of making one small improvement at a time, verifying, then repeating.

## The Rule

Change one thing. Verify. Repeat.

If you try to refactor everything at once, you will not know which change caused a breakage. Small steps are not slow — they are safe.

## Before You Start — Think About This

1. The code worked before you refactored. It still works after. Nothing changed for the user. What changed, and for whom?
2. If refactoring does not change behaviour, how do you know when you are done? What is the signal that a section no longer needs refactoring?
3. A colleague says: "Refactoring is a waste of time — just add the feature." They are not wrong that features matter. What would you say to them about why the state of the code affects how fast features can be added?

## When You're Stuck

- If you are not sure a refactoring is safe, run the program before and after and test every menu option. The program is small enough to test fully in 2 minutes.
- The hardest part of refactoring is stopping. Each fix reveals another. Set a limit: fix one thing per session, then stop and commit.

## Once It Works — Go Further

1. After Part C, try the overdue feature again. Did the diagnosis and fix make it easier? Write one sentence comparing the experience to Part A.
2. Look at the commit you made for the refactoring. The commit message should describe what changed structurally, not what behaviour changed. Write a commit message that someone could read in six months and understand exactly what you did and why.
