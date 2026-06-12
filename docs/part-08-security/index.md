---
title: Security
nav_order: 10
has_children: true
---

# Security

The rule in this section: experience the vulnerability before learning the fix.

You will store passwords in plain text. You will open the database file and read them. You will feel the risk. Then you will learn bcrypt.

## Topics

- Authentication (who are you?)
- Authorization (what are you allowed to do?)
- Sessions
- SQL Injection
- Password hashing with bcrypt
- HTTPS

## The Principle

Never learn a security tool without first understanding what attack it prevents.

## Exercises

- [8.1 The Database Leak](exercise-01-database-leak.md)
- [8.2 Add bcrypt](exercise-02-bcrypt.md)
- [8.3 SQL Injection](exercise-03-sql-injection.md)
- [8.4 Fix the Injection](exercise-04-fix-injection.md)
- [8.5 Sessions and Login](exercise-05-sessions.md)