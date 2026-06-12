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

### Step 1 — Add a librarians table

Add a `librarians` table to your schema:

```
id        INTEGER PRIMARY KEY
username  TEXT NOT NULL UNIQUE
password  TEXT NOT NULL
```

Write a small script (`add_librarian.py`) that:
- Asks for a username and password
- Inserts the record into `librarians` with the password stored exactly as typed

Add three librarians with realistic-looking passwords.

### Step 2 — Open the database and read the passwords

Close your Python script. Open `library.db` in DB Browser. Navigate to the `librarians` table.

Read the passwords.

You now have every librarian's password. You did not need to break any encryption. You did not need any special tools. You just opened a file.

### Step 3 — Think about the consequences

Write down answers to these questions:

1. If one of these librarians uses the same password for their email or their bank account — what does the attacker now have access to?
2. If you were the librarian and found out your password was stored this way — how would you feel about the engineer who built the system?
3. Is this the engineer's fault? They did not intend for the database to be stolen — they just did not think about what happens if it is. Is that an acceptable excuse?

### Step 4 — Understand what a fix requires

A good fix would mean: even if someone steals the database, they cannot read the passwords.

What would that require? Write a one-paragraph description of what a secure password storage system would need to do. Do not research solutions yet — think through it yourself first.

## Topics You Will Learn

- What plaintext storage means and why it is always wrong
- The difference between encryption (reversible) and hashing (one-way)
- Why password security affects users beyond just the application
- How to reason about threat models: "what happens if X is stolen?"

## Before You Start — Think About This

1. Could you encrypt the passwords instead of storing them in plain text? What problem would encryption solve — and what problem would remain? (Hint: who holds the encryption key, and where is that key stored?)
2. "Security through obscurity" — the idea that your system is safe because attackers do not know about it. Why is this not a reliable security strategy?
3. Most users reuse passwords across multiple sites. What does this mean for the responsibility of every site that stores passwords?

## Once It Works — Go Further

1. Look up a real data breach — for example, the LinkedIn breach of 2012 or the Adobe breach of 2013. What happened? How were passwords stored? How were they cracked? How many users were affected? Write a paragraph summary.
2. Before moving to Exercise 8.2: decide what the fix should be. Write your theory of how to store a password so that it can be verified without being readable. Then read about bcrypt and compare.
