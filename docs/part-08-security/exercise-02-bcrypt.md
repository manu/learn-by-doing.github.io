---
title: "8.2 Add bcrypt"
parent: Security
nav_order: 2
---

# Exercise 8.2 — Add bcrypt

## The Story

After Exercise 8.1, you know the problem: passwords in plain text can be read by anyone who accesses the database.

The solution is *hashing*. A hash function takes a password and produces a fixed-length string (the hash) that looks like random characters. The same password always produces the same hash. But the hash cannot be reversed — you cannot go from the hash back to the password.

When a user logs in, you hash the password they typed and compare it to the stored hash. If they match, the password is correct. The original password is never stored anywhere.

bcrypt is a hashing function designed specifically for passwords. It is intentionally slow — which makes it resistant to brute-force attacks.

## What to Do

### Part A — Install and explore bcrypt

bcrypt is a third-party Python library. Install it using pip.

Before using it in the library, run a small experiment first. Hash the same password twice. Compare the two hashes. Are they identical?

Now try to verify: take one of the hashes and check whether the original password matches it. Does it work, even though the two hashes look different?

Write down what you observe and think through why this is the case before moving on.

### Part B — Store hashes instead of passwords

Update `add_librarian.py` to hash the password before saving it to the database. The original password must not be stored anywhere.

Add a librarian. Open `library.db` in DB Browser. Look at the `password` column. What does it contain now?

### Part C — Build the login check

Write a function `verify_login(username, password)`. It should:
- Look up the librarian by username
- If no such username exists, the login fails
- If the username exists, check whether the provided password matches the stored hash

Test it manually: verify that the correct password succeeds and a wrong password fails. At no point during this check is the stored password ever turned back into readable text.

### Part D — Add the login page to Flask

Add two routes:
- A GET route that shows a login form with fields for username and password
- A POST route that calls `verify_login()` with the submitted data

On success, redirect to the home page. On failure, show the form again with an error message. Never show a specific message like "wrong password" — just "invalid username or password." Why? Think about what information you would be giving an attacker.

### Part E — Open the database one more time

Open `library.db` in DB Browser. Look at the `password` column.

Even if someone steals this database file right now, they cannot log in as a librarian. Write a short paragraph explaining why — and what an attacker would have to do to break it.

## Before You Start — Think About This

1. bcrypt produces a different hash each time, even for the same password. (Run it twice and compare.) How is it still possible to verify a password if the hash changes?
2. bcrypt is intentionally slow — it is designed to take a measurable amount of time (like 0.1 seconds) per verification. Why would you *want* a slow hash function for passwords?
3. If an attacker steals the bcrypt hashes, can they recover the passwords? What would they have to do? How does bcrypt's slowness affect the feasibility of this attack?

## When You're Stuck

- `bcrypt.gensalt()` generates a random "salt" — a value that makes each hash unique even for identical passwords. The salt is stored inside the hash string itself.
- Store the hash as bytes in the database, or convert to a string with `.decode()`. When verifying, convert back with `.encode()`.
- Never log passwords. Never print passwords. Never store passwords — only hashes.

## Once It Works — Go Further

1. Look up *rainbow tables* — precomputed tables of password hashes. How does the salt in bcrypt defeat rainbow table attacks?
2. bcrypt has a *cost factor* (the `12` in `$2b$12$...`). Increase it to `14`. How does this change the time taken to hash a password? When would you increase the cost factor in a real application?
