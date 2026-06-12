# Engineering Through One Project – Master Curriculum Notes

## Vision

Build a 2-year engineering curriculum for Amal around a single evolving project:

> Library Management System

The objective is not to teach Python syntax alone, but to teach:

- Engineering thinking
- Problem decomposition
- Architecture
- Data modeling
- Refactoring
- Security
- Networking
- Deployment
- AI-assisted development

---

# Core Philosophy

Every technology must be introduced only after the student experiences the problem it solves.

Pattern:

Problem
↓
Pain
↓
Technology
↓
Refactoring
↓
Architecture Review

Examples:

- Confusing file versions → Git
- Slow CSV search → SQL
- Plain-text passwords → bcrypt
- Large file → Modules
- Hard-to-maintain code → Refactoring
- Need for automation → Cron
- Need for shared access → Server
- Need for names instead of IPs → DNS

---

# Part 0 – Python Recall Bootcamp

Goal:
Reactivate Python knowledge already learned in Class 10.

Not a Python course.
A Python recall course.

Topics:

- Variables
- Input/output
- Functions
- Loops
- Lists
- Dictionaries
- CSV files

Sample exercises:

- Temperature converter
- Age calculator
- Prime checker
- Fibonacci
- Marks analysis
- Student records
- Book catalog CSV
- Mini Library

Rules:

- Keep programs small
- Avoid classes
- Avoid architecture discussions
- Focus on fluency

Final exercise:

Mini Library

Features:

- Add book
- List books
- Search books

Observe growing complexity.

---

# Part 1 – Engineering Mindset

Topics:

- File organization
- Naming
- Documentation
- README files
- Folder structure

Exercises:

Messy folder cleanup

Bad variable names

Write README

Key concept:

Information architecture

---

# Part 2 – Ownership and Responsibility

Inspired by Rust-style thinking.

Topics:

- Ownership
- Explicit data flow
- Avoid global variables
- References vs copies
- Resource ownership

Questions:

Who owns the data?

Who is allowed to change it?

Exercises:

Global variable disaster

Mutable vs immutable behavior

Ownership tracking

---

# Part 3 – Git

Teach why Git exists before commands.

Exercises:

library.py
library_final.py
library_final2.py
library_final_latest.py

Find the correct version.

Then introduce Git.

Concepts:

- History
- Commits
- Branches
- Issues
- Pull Requests

Important:

Teach meaning before commands.

---

# Part 4 – Refactoring

Definition:

Improve design without changing behavior.

Topics:

- Naming
- Functions
- Modules
- Separation of concerns

Exercises:

200-line file

500-line file

Duplicate code

Large switch statements

Questions:

What is difficult to change?

What is difficult to understand?

---

# Part 5 – Real Data

Use Open Library data.

Target:

- 10,000 books
- 50,000 books
- 100,000 books

Purpose:

Create real pain.

Observe:

- Startup time
- Search time
- Memory usage

Questions:

Why is it slow?

---

# Part 6 – SQL

Introduce only after CSV pain.

Topics:

- Schema design
- Relationships
- Joins
- Indexes
- Transactions

Teach:

Why SQL exists.

Not:

SQL syntax memorization.

Exercises:

Books

Members

Transactions

Library schema design

---

# Part 7 – Web Architecture

Teach request-response before Flask.

Architecture:

Browser
↓
Server
↓
Database

Exercises:

Observe browser requests

Use developer tools

Tiny HTTP server

Manual HTML responses

Then Flask

Important:

Flask is a framework.

Not the architecture.

---

# Part 8 – Security

Teach security through vulnerabilities.

Exercises:

Store plaintext passwords

Inspect database

Observe risk

Then introduce:

bcrypt

Topics:

- Authentication
- Authorization
- Sessions
- SQL Injection
- HTTPS

Principle:

Experience the vulnerability first.

---

# Part 9 – Networking

Topics:

- IP addresses
- DNS
- Subnet masks
- Routers
- Gateways

Use Raspberry Pi.

Important experiment:

library.elasticnode.com

Works on one laptop.

Fails on another.

Question:

Why?

This introduces DNS.

---

# Part 10 – Deployment

Use Raspberry Pi.

Topics:

- Nginx
- Reverse proxy
- Cron
- Backups
- Monitoring

Architecture:

Browser
↓
DNS
↓
Nginx
↓
Flask
↓
SQLite

---

# BIND DNS

Use:

elasticnode.com

Local records:

- library.elasticnode.com
- school.elasticnode.com
- git.elasticnode.com

Change laptop DNS to Raspberry Pi.

Observe behavior.

Teach:

Private DNS

Public DNS

Authoritative DNS

---

# Cron Jobs

Introduce only after automation is needed.

Examples:

- Daily reports
- Database backup
- Statistics generation

Concept:

Time-based events

---

# GitHub Workflow

Every feature:

Issue
↓
Branch
↓
Commit
↓
Pull Request
↓
Review

Teach:

- Bug reports
- Feature requests
- Refactoring issues

---

# Tailwind CSS

Use modern UI.

Topics:

- Dashboard
- Search pages
- Forms
- Reports

Concept:

Good user experience matters.

---

# AI Era Philosophy

AI can generate:

- Flask code
- SQL queries
- Git commands
- Tailwind layouts

Students should focus on:

- Architecture
- Security
- Data modeling
- Testing
- Refactoring
- Trade-offs

Question:

What problem was this technology invented to solve?

---

# Library Project Evolution

Version 1

CLI + CSV

Version 2

Git

Version 3

Refactoring

Version 4

10k+ books

Version 5

SQLite

Version 6

Web App

Version 7

Authentication

Version 8

Security

Version 9

Networking

Version 10

Deployment

Version 11

AI-assisted engineering

---

# GitHub Pages Structure

docs/
├── index.md
├── roadmap.md
├── glossary/
├── architecture-reviews/
├── diagrams/
├── datasets/
├── references/
├── issue-templates/
├── part-00-python-recall/
├── part-01-engineering-mindset/
├── part-02-ownership/
├── part-03-git/
├── part-04-refactoring/
├── part-05-real-data/
├── part-06-sql/
├── part-07-web/
├── part-08-security/
├── part-09-networking/
├── part-10-deployment/
└── part-11-ai-assisted-engineering/

---

# Final Goal

Amal should be able to explain:

Why Git exists

Why SQL exists

Why indexes exist

Why DNS exists

Why servers exist

Why request-response exists

Why bcrypt exists

Why refactoring exists

Why cron exists

Why web frameworks exist

Why architecture matters

And most importantly:

"What problem was this technology invented to solve?"
