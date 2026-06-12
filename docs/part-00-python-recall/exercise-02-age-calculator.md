---
title: "0.2 Age Calculator"
parent: Python Recall Bootcamp
nav_order: 2
---

# Exercise 0.2 — Age Calculator

## The Story

The school library has two types of membership: Junior (below 18) and Senior (18 and above). When a new member walks in and gives their birth year, the librarian needs to instantly know which category they fall into — and what their membership expiry year would be (memberships last 3 years).

This is the first time your program needs to *make a decision*.

## What to Build

Your program should ask for the person's name and birth year, then print their age, their membership type, and the year their membership expires.

```
Enter your name: Amal
Enter your birth year: 2008

Hello Amal!
Your age is: 18
Membership type: Senior Member
Membership valid until: 2029
```

And for someone younger:

```
Enter your name: Rohan
Enter your birth year: 2012

Hello Rohan!
Your age is: 14
Membership type: Junior Member
Membership valid until: 2029
```

## Topics You Will Need

- `input()` and `int()` — birth year will be a whole number
- Arithmetic — to calculate age from the current year
- `if` / `else` — to decide between Junior and Senior
- Variables — to store name, age, membership type, expiry year
- `print()` with f-strings or string concatenation

## Before You Start — Think About This

1. You know the current year is 2026. But what if you run this program next year? Should you hardcode `2026` in your code, or is there a better way?
2. If someone was born in 2008, are they definitely 18 years old in 2026? What if their birthday hasn't come yet this year? (For now, just subtract — we'll ignore months.)
3. What is the condition that separates a Junior from a Senior? Write it in plain English before writing any code.
4. The expiry year is the same regardless of membership type. Where should that calculation go in your program?

## When You're Stuck

- `int()` converts text like `"2008"` into the number `2008`. Without it, subtracting years will give you an error.
- An `if/else` block looks like: if (condition is true) do one thing, else do the other thing. The condition uses a comparison operator — look up `<`, `>`, `<=`, `>=`.
- To get today's year automatically without hardcoding it, look up Python's `datetime` module — specifically `datetime.date.today().year`.

## Once It Works — Go Further

1. Add a third membership type: if someone is 60 or older, they get "Senior Citizen" membership with a 5-year validity instead of 3.
2. Ask for the birth month as well and calculate the age more accurately — if their birthday hasn't passed yet this year, subtract one from the age.
3. Make the program loop so it can process multiple new members one after another until the librarian types "done".
