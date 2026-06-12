---
title: "0.4 Marks Analysis"
parent: Python Recall Bootcamp
nav_order: 4
---

# Exercise 0.4 — Marks Analysis

## The Story

The library runs a monthly reading quiz. Students answer questions about books they borrowed, and the librarian records their scores. After every quiz, the librarian wants a quick summary: who scored highest, who scored lowest, what the class average was, and who passed (60 or above) and who did not.

Right now the librarian does all of this by hand. Your program will do it instantly.

This exercise introduces *lists* — the way Python stores many values together so you can work with them as a group.

## What to Build

Your program should ask for the number of students, then ask for each student's name and score. After all entries, it prints a full analysis.

```
How many students? 5

Student 1 name: Amal
Student 1 score: 85

Student 2 name: Priya
Student 2 score: 72

Student 3 name: Rohan
Student 3 score: 55

Student 4 name: Fatima
Student 4 score: 91

Student 5 name: Arjun
Student 5 score: 48

--- Quiz Results ---
Total students : 5
Highest score  : Fatima — 91
Lowest score   : Arjun — 48
Class average  : 70.2
Passed (≥ 60)  : Amal, Priya, Fatima
Failed (< 60)  : Rohan, Arjun
```

## Topics You Will Need

- `input()`, `int()`, `float()` — for reading names and scores
- Lists — to store all the names and all the scores
- `for` loop — to go through each student
- `max()`, `min()`, `sum()`, `len()` — Python's built-in list functions
- `if` / `else` inside a loop — to separate pass from fail

## Before You Start — Think About This

1. You have two things to store per student: a name and a score. You could have one list for names and one for scores. How would you make sure they stay in sync (that `names[0]` and `scores[0]` always belong to the same student)?
2. `max()` gives you the highest number — but how do you find *whose* score that was? Think about how the position of a value in one list relates to the same position in another list.
3. What is the average? Write the formula in plain English before writing any code.
4. The pass list and fail list are built by going through every student and checking their score. This happens *after* all students are entered, not during entry. Why might it be cleaner to separate those two steps?

## When You're Stuck

- An empty list is just `[]`. You can add things to a list with `.append()`.
- To loop through a list, use `for item in my_list:`. To loop with position numbers, use `for i in range(len(my_list)):`.
- `max(scores)` gives the highest score. To find the index (position) of that score, use `.index()`. Then use that same index to look up the name.
- To build a comma-separated list of names, look up `", ".join(list_of_names)`.

## Once It Works — Go Further

1. Sort the results and print a ranked leaderboard from highest to lowest score.
2. Add letter grades: A (90+), B (75–89), C (60–74), F (below 60). Print each student's grade next to their name.
3. If there is a tie for highest or lowest score, your current program only shows one name. Fix it to show all tied students.
