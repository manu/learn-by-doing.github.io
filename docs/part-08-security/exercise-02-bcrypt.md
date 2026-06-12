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

### Step 1 — Install bcrypt

```
pip install bcrypt
```

### Step 2 — Update the registration script

Modify `add_librarian.py` so that instead of storing the plaintext password, it:
1. Hashes the password using bcrypt
2. Stores the hash in the database

After adding a librarian, open DB Browser. The `password` column should now contain something like:
```
$2b$12$LQv3c1yqBWVHxkd0LHAkCOYz6TtxMQJqhN8/lfKZ7hN...
```

That is the bcrypt hash. The original password is gone.

### Step 3 — Build login verification

Write a function `verify_login(username, password)` that:
1. Looks up the librarian by username in the database
2. If not found, returns `False`
3. If found, uses bcrypt to check whether the provided password matches the stored hash
4. Returns `True` if it matches, `False` otherwise

Test it: correct password should return `True`, wrong password should return `False`.

### Step 4 — Integrate with the Flask login route

Add a login page to the web app:
- `GET /login` — shows a login form (username + password fields)
- `POST /login` — calls `verify_login()` with the submitted data, redirects to the home page on success, shows an error on failure

### Step 5 — Open the database again

Open `library.db` in DB Browser. Look at the `password` column again.

Even if someone steals this database, the passwords cannot be read. They can try to guess — but bcrypt is slow enough that guessing millions of passwords takes a very long time.

## Topics You Will Need

- `bcrypt.hashpw(password.encode(), bcrypt.gensalt())` — hash a password
- `bcrypt.checkpw(password.encode(), stored_hash)` — verify a password
- Why `.encode()` is needed (bcrypt works with bytes, not strings)
- Flask `request.form` — reading POST form data
- `redirect()` and `url_for()` in Flask

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
