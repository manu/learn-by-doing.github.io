---
title: "4.7 Before and After"
parent: Refactoring
nav_order: 7
---

# Exercise 4.7 — Before and After

## The Story

You have spent several exercises improving the Mini Library. The program does exactly what it did before. From the outside — from the user's perspective — nothing has changed.

But something has changed. The question is: can you describe what?

This is the final exercise of Part 4. It is not about writing more code. It is about stepping back and seeing what the refactoring actually accomplished — in concrete terms, not vague ones. "It's cleaner" is not enough. An engineer should be able to say precisely what is better, why it is better, and what would have been harder without it.

This skill — the ability to articulate architectural decisions and their consequences — is what separates engineers who can work in teams from engineers who can only work alone.

## What to Do

### Part A — Retrieve the original

Find the original 300-line `library.py` in your Git history. It exists there — you committed it before refactoring.

Run `git log --oneline` and find the commit where the library was still a single file with all features. Note the commit hash.

Use Git to look at that file as it was then. Do not check it out — just view it.

Now you have two versions: what it was, and what it is now. Put them side by side in your mind.

### Part B — Measure the difference

Do not use words like "cleaner", "better", or "more readable." Use specific, measurable observations.

Answer each of these:

1. **Length of longest function:** What was the longest function in the original? What is the longest now?
2. **Number of responsibilities per file:** How many different concerns did the original file handle? How many does each current file handle?
3. **Lines to read before adding a feature:** In the original, how many lines would you need to understand before safely adding "mark book as lost"? In the current version, which file would you open, and roughly how many lines does that file have?
4. **Places to change for a format change:** If the CSV column order changes, how many files need updating in the original? In the current version?
5. **Testability:** In the original, could you test the search function without running the whole program? Can you now?

Write specific numbers where possible.

### Part C — Write the architecture note

Write a short document (half a page) describing the current architecture of the Mini Library. Explain:

- What files exist and what each one is responsible for
- How data flows through the system (where it enters, how it moves, where it is stored)
- What the main design decisions were and why

Write this for a new team member who has never seen the code. They should be able to read your note, then open the files and immediately know where to look for any given feature.

This document is called an **architecture note**. Real engineering teams maintain these. They become more valuable as the project grows and the number of people working on it increases.

### Part D — What you would do next

Every codebase has more to improve. Based on your diagnosis in Exercise 4.5 (code smells), write a short list of what you would refactor next if you had more time.

For each item, write:
- What the problem is
- What technique you would use
- What specific improvement you expect

This list is a backlog of technical debt. In a real project, it would live as GitHub issues.

### Part E — The honest retrospective

Answer these questions honestly:

1. Was every refactoring you did worth the time it took? Were any of them unnecessary — did you over-engineer something that was fine?
2. Did you make the program harder to understand in any way? (Sometimes splitting things up creates too many small pieces and makes the whole harder to see.)
3. What would you do differently if you started the Mini Library again today, knowing what you know now?

There are no right answers. The value is in thinking carefully about trade-offs.

## Before You Start — Think About This

1. A new engineer joins the team and needs to fix a bug in the search feature. In the original code, where would they start? In the refactored code, where would they start? How long would each take?
2. Refactoring takes time. In a real project with deadlines, how do you justify the time spent? What would you say to a manager who asks "why are we rewriting working code?"
3. The program behaves identically before and after all this work. The user noticed nothing. Who was the refactoring for?

## When You're Stuck

- To view a file at a specific past commit without changing your current code: `git show <hash>:path/to/file.py`
- If you cannot find the original single-file version, look for the commit with the message you wrote when you first finished the Mini Library.
- The architecture note does not need to be long. Three clear paragraphs describing three things (files, data flow, decisions) is better than a ten-paragraph document full of vague sentences.

## Once It Works — Go Further

1. Compare your architecture note to the original code. Is there anything in the original that your note does not explain? That gap means your architecture note is incomplete — or that the original did something the refactoring lost.
2. Read the architecture note to someone who has never seen the project. Where do they get confused? That confusion is a gap in either the note or the design itself.
