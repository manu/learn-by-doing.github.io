---
title: "4.5 Code Smells"
parent: Refactoring
nav_order: 5
---

# Exercise 4.5 — Code Smells

## The Story

A doctor can look at a patient and notice warning signs before running any tests — pale skin, laboured breathing, a certain kind of posture. These signs do not diagnose the disease, but they say: *something here needs investigation*.

Code has the same kind of warning signs. Engineers call them **code smells** — patterns in code that consistently signal a deeper problem. A smell does not mean the code is wrong. It means: *look more carefully here*.

Learning to recognise smells is the first step in refactoring. Before you can fix a problem, you have to know you have one. The exercises so far gave you specific techniques — extract functions, split modules, remove duplication. This exercise teaches you to see which technique a piece of code is asking for.

## The Smells

Study each smell. For each one, think about whether you have seen it in your Mini Library.

---

**The Long Function**
A function that is longer than you can read without scrolling. No fixed line limit — the question is whether you can hold the whole function in your head at once. If not, it is doing too many things.
*Technique needed:* Extract functions.

---

**The God Function**
A function that orchestrates everything: reads input, validates it, calls other functions, handles errors, updates the file, and prints a result. It knows too much about everything. A change anywhere in the program may require changing this function.
*Technique needed:* Extract functions; separate concerns.

---

**The Mystery Variable**
`x`, `d`, `tmp`, `data`, `result`. A variable name that forces the reader to trace back to where it was created to understand what it holds. The name should make the value's purpose obvious without context.
*Technique needed:* Rename.

---

**The Magic Number**
`if year > 1900` — what is 1900? Why 1900? A raw number with meaning, embedded directly in code. Two months later, nobody knows why 1900 was chosen, and changing it requires finding every occurrence.
*Technique needed:* Extract to a named constant.

---

**The Comment that Explains What**
```
# loop through all books and find matching ones
for book in books:
    if query in book["title"]:
```
The comment tells you what the code does — but you can already see that from the code. What would a good comment say instead? Why this loop exists, what edge case it handles, what decision was made here.
*Technique needed:* Rename the surrounding function or variable so the comment becomes unnecessary.

---

**Parallel Duplication**
You add a new book status — "lost". You update the add function. You update the display. You update the search. You update the CSV headers. Five places. Every time a new status is added, all five must change together. They are parallel — always updated as a group.
*Technique needed:* Find the single place where status is defined and have everything else derive from it.

---

**The Afraid-To-Delete Function**
A function that exists in the file but is never called. You are not sure if it is needed so you leave it. It makes the file longer and more confusing. Old, unused code is not a safety net — it is noise.
*Technique needed:* Delete it. Git history holds it if you ever need it back.

---

**The Long Parameter List**
A function that takes six parameters. When you call it, you have to look up what each one means. When you read the call, you see six values with no labels telling you which is which.
*Technique needed:* Group related parameters into a dictionary or structure; or question whether the function is doing too much.

---

## What to Do

### Part A — The smell audit

Go through your Mini Library modules — every file. For each smell above, mark whether you find it, and write down the specific location (function name, line number, or a brief description).

This is a written diagnosis. Be honest. Finding smells is not failure — every codebase has them. The failure is not looking.

### Part B — Priority

Not all smells are equal. For each one you found, write one sentence: how much does this smell slow you down or create risk? Rank them from most painful to least.

Refactoring should pay off. Fix the most painful smell first.

### Part C — One smell, one fix

Pick the highest-priority smell. Apply the appropriate technique. Verify the program is identical before and after.

Write a commit message that names the smell and describes what you did. Not "refactor code" — "Remove magic number 1900 by extracting ARCHIVE_THRESHOLD constant."

### Part D — The smell you will not fix yet

Pick one smell that is real but not yet worth fixing — perhaps because the code is small enough that it does not yet hurt. Write down: what would need to change (a new feature, a new team member, a certain size) before this smell would become painful enough to fix?

## Before You Start — Think About This

1. A comment that says "# add book to list" is a smell. But a comment that says "# CSV has no header — stripped during school system export" is not. What is the difference, and what does it tell you about when comments are needed?
2. Deleting an unused function feels risky. What does Git's history tell you about how permanent "delete" really is?
3. Two engineers look at the same long function. One says "it works, leave it." The other says "it's a smell, extract it." Who is right — and what question would help you decide?

## When You're Stuck

- If you cannot find a smell, it may be because you have already fixed it in earlier exercises. That is progress, not a failure to complete the exercise.
- The fear of deleting unused code is common. Run the program's full menu after deleting. If nothing breaks, the function was not used.
- `git grep "function_name"` searches the entire codebase for any mention of a name. Use it to check whether a function is truly unused before deleting it.

## Once It Works — Go Further

1. The word "smell" was popularised by Martin Fowler in his book *Refactoring*. Look up his original list of code smells. Are any on his list that are not on this page? Which ones apply to your Mini Library?
2. Some smells only appear at larger scale — a "God Class" that knows everything, for example. Your Mini Library may not have classes yet. But think ahead: when classes appear in Part 6 (SQL) and Part 7 (Web), which of these smells could appear at the class level?
