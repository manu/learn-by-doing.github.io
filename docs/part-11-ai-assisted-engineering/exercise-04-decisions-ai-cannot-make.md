---
title: "11.4 Decisions AI Cannot Make"
parent: AI-Assisted Engineering
nav_order: 4
---

# Exercise 11.4 — Decisions AI Cannot Make

## The Story

Over the past two years, you have built a complete library system: command-line to web app, CSV to SQLite, development to deployment. The librarian is happy. The system works.

Now you are being asked to make a series of decisions about what comes next. The school wants to expand the library system to a second branch — a new building across the road. Both branches should share the same book catalog, but each should manage its own members and loans.

You ask an AI assistant. It gives you three approaches with code examples for each. All three look reasonable. All three would work.

But you are the engineer. The AI cannot choose for you. It does not know your constraints, your timeline, your skills, or what "good enough" means for this school.

## What to Do

### Part A — Understand the three approaches

An AI has suggested these options for the two-branch expansion:

**Option 1: Two separate databases, synchronized nightly**
Each branch has its own `library.db`. A cron job copies the books table from branch A to branch B every night.

**Option 2: One shared database on the Raspberry Pi, both branches connect to it**
Both branches run Flask. Both connect to the same SQLite file on one Pi over the network.

**Option 3: Split the database — shared books, separate members and loans**
One database for the shared catalog. Two separate databases for members and loans (one per branch). Flask at each branch joins across them.

For each option, write down:
- What happens when the internet/network connection between buildings goes down?
- What happens if one branch's server fails?
- How hard is it to add a third branch later?
- What skills or infrastructure does it require?

### Part B — Apply what you have learned

Each of the three options has problems that you have already encountered during this curriculum:

- Synchronization: what did you learn about two sources of truth in Part 5 and Part 6?
- Shared network database: SQLite is designed for single-machine use. What did you learn about concurrent access in Part 6?
- Split databases: how does a JOIN work when the two tables are in different database files?

For each problem you identify, write which part of the curriculum taught you why it is a problem.

### Part C — Make the recommendation

Write a recommendation for which approach to use. Your recommendation must include:
1. Which option you recommend and why
2. The specific risks of your chosen option and how you would mitigate them
3. Which option you would recommend against, and why it is worse
4. What additional information you would need to make a more confident decision

The AI cannot make this recommendation because it does not know: the school's budget, the network reliability between buildings, the librarian's technical skills, or how important uptime is. You know more about the context than the AI does.

### Part D — Reflect on the AI's role

After completing the exercise, write a short paragraph on this question:

The AI gave you three options with code, architecture diagrams, and pros/cons lists. It was helpful. But it could not make the final decision.

What specifically did you need to know — that the AI does not know and cannot know — to make this decision? What does that tell you about where AI fits in the engineering process?

## Before You Start — Think About This

1. When an AI gives you three options and says "all of these are valid approaches," what is it actually saying? What is it not saying?
2. Trade-offs require knowing your constraints. What constraints does the AI have no access to in this scenario?
3. After two years of building this system, you know things about the library that no AI knows — you have talked to the librarian, you know what breaks, you know the school's budget. How valuable is that knowledge compared to the AI's ability to generate code?

## When You're Stuck

- If you are unsure how to evaluate an option, trace through a specific failure scenario. What would happen to real students and the real librarian if that failure occurred during a busy school day?
- "Good enough" is a legitimate engineering answer — not everything needs to be optimal. What is "good enough" for a school library with two branches?

## Once It Works — Go Further

1. Look up CAP theorem — a theorem in distributed systems that says you cannot simultaneously have consistency, availability, and partition tolerance. Which of the three options sacrifices which property?
2. Ask an AI assistant to recommend a database system for this two-branch scenario. What does it recommend? Do you agree? What assumptions did it make that you would challenge?
