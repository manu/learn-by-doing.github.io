---
title: "8.1 The Database Leak"
parent: Security
nav_order: 1
---

# Exercise 8.1 — The Database Leak

## The Story

The library web app now has users — librarians who log in to manage books and loans. They need passwords.

You add a `librarians` table to the database with columns `username` and `password`. When a librarian registers, you save their password directly to the database. It works perfectly.

Now imagine what happens when the database file is stolen. Someone copies `library.db` off the server. They open it in DB Browser. They see every username and every password, in plain text, for every librarian who ever registered.

This exercise makes you feel that moment — so that you understand exactly what bcrypt prevents.

## What to Do

### Part A — Add librarians to the system

The library web app needs a `librarians` table. Each librarian has a username and a password. Design the table columns yourself (you have done schema design in Part 6).

Write a small script called `add_librarian.py` that asks for a username and password and saves both into the database, exactly as typed.

Add three librarians with passwords that look like real passwords — the kind someone might actually use.

### Part B — Open the database as an attacker

Close your Python script. Open `library.db` in DB Browser. Navigate to the `librarians` table.

Read the passwords.

Write down what you see. You did not break any encryption. You did not use any special tools. You opened a file.

### Part C — Reason through the consequences

Write down answers to these three questions:

1. Most people use the same password for multiple accounts — email, banking, social media. If this database were stolen, what else could the attacker access?
2. If you were one of the librarians and found out your password was stored like this — how would you feel about the engineer who built the system?
3. The engineer did not intend for the database to be stolen. They simply never thought about what happens if it is. Is that an acceptable excuse?

### Part D — Design the fix yourself

Before reading anything about how passwords are actually secured, write a one-paragraph description of what a secure password storage system would need to do.

The constraint: even if someone steals the database, they should not be able to read the passwords. How would you store a password so that it can be verified later — but not read?

Keep this paragraph. After Exercise 8.2, come back and compare your idea to what bcrypt actually does.

## Before You Start — Think About This

1. Could you encrypt the passwords instead of storing them in plain text? What problem would encryption solve — and what problem would remain? (Hint: who holds the encryption key, and where is that key stored?)
2. "Security through obscurity" — the idea that your system is safe because attackers do not know about it. Why is this not a reliable security strategy?
3. Most users reuse passwords across multiple sites. What does this mean for the responsibility of every site that stores passwords?

## Once It Works — Go Further

1. Look up a real data breach — for example, the LinkedIn breach of 2012 or the Adobe breach of 2013. What happened? How were passwords stored? How were they cracked? How many users were affected? Write a paragraph summary.
2. Before moving to Exercise 8.2: decide what the fix should be. Write your theory of how to store a password so that it can be verified without being readable. Then read about bcrypt and compare.
