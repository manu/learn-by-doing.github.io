---
title: "4.6 Naming as Design"
parent: Refactoring
nav_order: 6
---

# Exercise 4.6 — Naming as Design

## The Story

A student finishes her library project and asks a friend to review it. The friend opens the code and immediately asks: "What is `proc_bk`?"

"Process book," the student says.

"What does process mean?"

"It... validates it. And adds it. And saves it."

"So it does three things?"

"I guess."

That conversation happened in code review. But it started with a name. The name `proc_bk` compressed an entire design problem into eight characters. Naming it well would have revealed the problem before the code was written.

**Naming is not labelling.** Naming is design. When you cannot find a good name for something, it is almost always because the thing you are trying to name is doing too much, or has no clear identity, or belongs in two places at once. The difficulty of naming is a signal — it points at a structural problem.

## What to Do

### Part A — The naming audit

Read every function and variable name in your Mini Library. For each one, ask three questions:

1. Does the name tell you what the thing IS (for variables) or what it DOES (for functions)?
2. If someone read only the name — not the code — would they know what to expect?
3. Is the name accurate? A function called `get_books` that also validates and filters is not just incomplete — it is misleading.

Write a list: name, the question it fails (if any), and a proposed better name.

### Part B — Rename one and follow the chain

Pick the worst name. Rename it.

Now read the code around it. Does the new name change how you think about the surrounding code? Does it make a nearby variable name look wrong by comparison? Does it reveal that the function is doing more than its new name suggests?

Rename what it reveals. Then read again. Keep following the chain until the names stabilise.

Write down: how many things did you rename because of the first rename?

### Part C — The naming pressure test

For every function, cover its body and read only its name. Then write one sentence predicting what it does.

Now uncover the body. Compare your prediction to reality.

Every mismatch is a naming problem. Either the function does something different from what its name says (the name is wrong), or the function does too much for any name to fully describe (the function is wrong).

Fix every mismatch: either rename, or split the function so each part can be correctly named.

### Part D — When you cannot find a name

Take the hardest function to name in your library — the one where you keep writing names that are either too vague or too specific.

Instead of forcing a name, write a one-paragraph description of what the function does. Read what you wrote. Count the verbs. If there is more than one verb, the function is doing more than one thing.

Split it along the verb boundaries. Then name each piece. Small functions are almost always easier to name than large ones.

## Before You Start — Think About This

1. `process`, `handle`, `manage`, `do` — these verbs appear in many function names. What do they have in common, and why are they warning signs?
2. A variable name like `books` is good for a list of all books in the library. But if that same variable is later filtered down to only available books, is `books` still the right name? What does a wrong name after a transformation cost you?
3. Engineers sometimes distinguish between names that describe *what something is* versus names that describe *how it is implemented*. For example, `book_list` (what it is) versus `csv_rows` (how it is stored). Which kind of name ages better as the code changes?

## When You're Stuck

- If you cannot name a function without using "and" — it is doing two things. Split it.
- If you cannot name a variable without writing a sentence — the variable is holding something too complex. Is it one thing, or multiple things bundled together?
- Read the function name aloud. Does it sound like something a librarian would say? ("Search for a book." "Remove an overdue loan.") If it sounds like programmer jargon ("Process the entity"), the naming is not yet done.

## Once It Works — Go Further

1. Look at the Python standard library — open the `csv` module documentation. Read just the function names. Do they tell you what each function does without reading the descriptions? This is the naming standard to aim for.
2. Find one function where your naming audit uncovered a structural problem — a function that could not be named well because it was doing two things. Write one paragraph: what was the function doing, what were you trying to call it, and what did splitting it reveal about the design?
