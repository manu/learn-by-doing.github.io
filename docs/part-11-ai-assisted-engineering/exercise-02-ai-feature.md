---
title: "11.2 Build a Feature with AI"
parent: AI-Assisted Engineering
nav_order: 2
---

# Exercise 11.2 — Build a Feature with AI

## The Story

You need to add a new feature to the library: a dashboard page that shows key statistics — total books, total members, total active loans, overdue count, and a list of recently added books.

You will use an AI assistant to help write the code. But you are the engineer — the AI is your tool, not your replacement. Every line it produces goes through your understanding before it goes into the codebase.

## What to Do

### Part A — Write the specification before touching AI

Before opening any AI assistant, write a complete specification for the dashboard:
- What data should it display? (List every number, every table, every list)
- Where does each piece of data come from? (Which database table, which query)
- What should the URL be?
- What should happen when there are no loans? No members? The database is empty?

This specification is the standard the feature must meet. If you cannot describe what you want precisely, the AI will fill in the gaps with assumptions — and those assumptions may be wrong.

### Part B — Use AI to generate a starting point

Prompt the AI with your full specification. Ask it to write the Flask route, the database queries, and the template.

Pay attention to what the AI assumed. Did it assume your database schema? Your URL structure? Your template names? Are any of those assumptions incorrect?

### Part C — Read every line before using it

Go through the AI's output one piece at a time. For each section, answer:
- Do I understand what this does? If not, ask the AI to explain it — then verify the explanation yourself.
- Is this the right approach? Are there problems you recognize from earlier in the curriculum?
- Does this match the specification you wrote in Part A?

Do not copy anything you cannot explain. If you cannot explain it, you cannot fix it when it breaks.

### Part D — Integrate, test all cases, fix problems

Integrate the code into the library. Test every case in your specification:
- Normal: data exists
- Edge: no loans this week
- Edge: some books overdue, some not
- Edge: the database is completely empty

Find and fix every problem before considering the feature done.

### Part E — Measure the real cost

Write a short honest assessment:
- How long did writing the specification take?
- How long did reviewing and fixing the AI's output take?
- How long would the feature have taken if you had written it yourself from the start?
- What did AI actually save? What did it not save?

## Topics You Will Learn

- Writing a specification before generating code
- Prompt engineering: how to describe what you want precisely
- Code review of AI-generated output
- Testing to verify correctness, not just to verify "it runs"
- Understanding that AI accelerates implementation, not thinking

## Before You Start — Think About This

1. If you copied the AI's code without reading it and it worked — would you know *why* it worked? What would happen the first time it needed to be changed?
2. The AI does not know your database schema, your project structure, or your security requirements. What information should you include in the prompt to get useful output?
3. AI makes confident-sounding mistakes. How do you distinguish between an AI that is correct and one that is confidently wrong?

## When You're Stuck

- If the AI's code does not work, debug it yourself before asking AI again. What exactly is failing? What did you expect? What happened instead?
- If the AI's code works but you do not understand it, do not move on. Ask AI to explain each part until you understand it, then verify the explanation by tracing through the logic manually.
- The specification you wrote in Step 1 is the acceptance criteria. The feature is done when it satisfies the specification — not when it runs without errors.

## Once It Works — Go Further

1. Ask the AI to write unit tests for the dashboard route. Review those tests the same way you reviewed the code. Are they actually testing the right things? Do they cover the edge cases?
2. Try using AI for a feature without writing a specification first. Compare the experience to this exercise. What was different about the output? What was harder?
