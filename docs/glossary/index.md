---
title: Glossary
nav_order: 14
---

# Glossary

**bcrypt** — A password hashing function. Stores a one-way fingerprint of a password so the original is never saved. Even if the database is stolen, passwords remain protected.

**DNS** — Domain Name System. Translates human-readable names like `library.elasticnode.com` into IP addresses that computers use to connect.

**Git** — A version control system. Records every change to a project with a message, author, and timestamp so the full history can be reviewed or reversed.

**HTTP** — HyperText Transfer Protocol. The language browsers and servers use to communicate. A browser sends a *request*; the server sends a *response*.

**Index (SQL)** — A data structure that makes lookups fast. Without an index, a search scans every row. With an index, it jumps directly to the answer.

**Nginx** — A web server often used as a reverse proxy — sitting in front of a Flask app and forwarding requests to it.

**SQL** — Structured Query Language. The language used to read and write data in a relational database.

**SQLite** — A lightweight database that stores everything in a single file. Used in this project before upgrading to a server database.

**bcrypt** — see above.

**Transaction** — A group of database operations that either all succeed or all fail together. Prevents data corruption from partial updates.
