# Engineering Through One Project — Master Notes

Student: Amal (11th standard, ~16 years old)
Duration: 2 years
Project: Library Management System (grows from CLI script to deployed web app)
Site: https://manu.github.io/learn-by-doing.github.io

---

## Core Philosophy

Software engineering is not about writing Python. It is about solving problems.
Python is just the current tool. The skill is problem decomposition, asking the right
questions, and knowing why a technology exists before learning how to use it.

**The guiding question for every technology:**
> "What problem was this technology invented to solve?"

**The teaching pattern — every part follows this arc:**

```
Problem (Amal experiences it directly)
  ↓
Pain (he feels why the current approach does not scale)
  ↓
Technology (introduced as the answer to the pain)
  ↓
Refactoring (clean up the solution)
  ↓
Architecture Review (step back and see the whole system)
```

**Real-world examples used in the introduction:**
- Hunger → Zomato (coordination between customer, restaurant, delivery)
- Medical risk → Drug interaction checking in hospitals
- Scale → Satellite crop monitoring for farmers
- Coordination → Adaptive traffic lights
- Enforcement → Illegal fishing detection via GPS
- Access → Translation into 7,000 languages

---

## Things Deliberately Not Taught Early

This section preserves the philosophy as the curriculum grows.

| Thing | Taught only after |
|-------|------------------|
| Classes and OOP | Data modeling is understood through dicts and lists first |
| Flask | HTTP request-response is understood manually first |
| SQL | CSV pain at 10,000+ records has been experienced |
| bcrypt | A plaintext password database has been inspected |
| Git commands | Version confusion with identically-named files has been felt |
| DNS | A hostname that works on one laptop and fails on another |
| Indexes | A slow search through 100,000 rows has been waited through |
| Cron | A manual repetitive task has been done enough times to hurt |
| Architecture diagrams | The system has grown complex enough to need one |

---

## Exercise Template

Every exercise follows this exact structure. No Python code is ever given.
Amal writes everything himself.

```
## The Story
Real-world reason this problem exists.
Connected to the library project where possible.

## What to Build
Sample terminal input/output showing the expected behaviour.
No code. Just the target.

## Topics You Will Need
Explicit bullet list of Python concepts needed.
Named so he knows exactly what to study if stuck.

## Before You Start — Think About This
3–4 questions to reason through on paper before touching the keyboard.

## When You're Stuck
2–3 directional hints. Point toward an idea, not at an answer.

## Once It Works — Go Further
2–3 extension challenges to push past the minimum requirement.
```

---

## Part 0 — Python Recall Bootcamp

**Goal:** Reactivate Python from Class 10. Not a new course — a recall course.

**Rules:**
- Programs are 20–50 lines maximum
- No classes, no frameworks
- Focus on fluency and clarity

**Exercise arc — one new concept per exercise:**

| # | Exercise | New Concept |
|---|----------|-------------|
| 0.1 | Temperature Converter | variables, input, arithmetic |
| 0.2 | Age Calculator | if/else, int conversion, current year |
| 0.3 | Fibonacci Shelf Numbers | while loop, multiple updating variables |
| 0.4 | Marks Analysis | lists, max/min/sum/len, for loop |
| 0.5 | Student Records | dictionaries, list of dicts, search |
| 0.6 | Book Catalog | file reading, split, strip, formatting |
| 0.8 | Prime Checker | modulo, break, efficiency thinking |
| 0.26 | Mini Library | everything combined — menu, CSV, search |

**Mini Library requirements (the culminating exercise):**
- Menu: Add book / List all / Search by title / Quit
- Stores books in `library.csv`
- Survives program restart (loads file on start)
- Partial title search (case-insensitive)
- After it works: Amal observes what is hard to read, hard to change,
  and what would break if features were added → this transitions to Part 1

---

## Part 1 — Engineering Mindset

**Key idea:** Code is written once. It is read many times.

**Exercises:**
- 1.1 Messy Folder — reorganize a chaotic project folder, write a README,
  rename every variable that doesn't describe what it holds

**Concepts:**
- File and folder organization
- Naming conventions (variables, files, functions)
- README writing (what, how to run, dependencies, what files it needs)
- Information architecture

---

## Part 2 — Ownership and Responsibility

**Key idea:** Who owns the data? Who is allowed to change it?
Inspired by Rust's memory ownership model, applied to Python design.

**Exercises:**
- 2.1 Global Variable Disaster — a broken program where functions silently
  modify globals; find the bugs, understand why they happen, rewrite
  with parameters and return values

**Concepts:**
- Global vs local scope
- Explicit data flow through function parameters
- A function should be predictable: same input → same output, no side effects

---

## Part 3 — Git and History

**Key idea:** Teach why Git exists before any commands.

**Exercise arc:**
1. Present folder with: library.py, library_final.py, library_final2.py,
   library_final_FIXED.py, library_final_latest.py
2. Find the correct version — feel the pain
3. Write down what was confusing
4. Then introduce Git as the answer

**Concepts:** history, commits, branches, issues, pull requests

**GitHub workflow to teach and practice:**
```
Issue → Branch → Commit → Pull Request → Review → Merge
```
Every feature added to the library system should follow this workflow.
Teach: bug reports, feature requests, refactoring issues.

**Commit message philosophy:**
A commit answers: "What meaningful change happened?"
- Bad: `initial commit`, `changes`, `fix`
- Good: `Define engineering curriculum and library project vision`
- Good: `Add Part 0 Python recall bootcamp`
- Good: `Replace CSV with SQLite for book storage`

---

## Part 4 — Refactoring

**Definition:** Improve the design of code without changing what it does.

**Exercise arc:**
1. Given: the Mini Library grown to 200+ lines with duplicated logic
2. Identify: what is hard to read, hard to change, what breaks if touched
3. Refactor: better names, split functions, separate concerns into modules
4. Verify: behaviour is identical before and after

**Concepts:** naming, functions, modules, separation of concerns, duplication

**Key questions to ask of any code:**
- What is difficult to understand?
- What would be hard to change?
- What would break if I changed this one thing?

---

## Part 5 — Real Data

**Key idea:** Create real pain before introducing databases.

**Data source:** Open Library (open dataset, free download)

**Exercise arc:**
1. Load 10,000 books from CSV — observe startup time and search time
2. Load 50,000 books — measure the difference
3. Load 100,000 books — the program becomes unusable
4. Ask: why is it slow? What would need to change?

**What to measure and observe:**
- Startup time (how long before the menu appears)
- Search time (how long to find one title in 100,000)
- Memory usage (watch Task Manager)

---

## Part 6 — SQL as a Solution

**Introduced only after the CSV pain of Part 5.**

**Library schema:**
```
books        (id, title, author, year)
members      (id, name, email)
transactions (id, book_id, member_id, date, returned)
```

**Exercise arc:**
1. Why CSV hurts — articulate the specific limitations experienced in Part 5
2. Design the schema — draw tables and relationships before writing SQL
3. Migrate data — move 10,000 books from CSV into SQLite
4. Queries — search, join transactions with members, find overdue books
5. Indexes — measure search speed before and after adding an index

**Concepts:** schema design, relationships, joins, indexes, transactions

---

## Part 7 — Web Architecture

**Key idea:** Flask is a framework, not an architecture.
Understand the architecture before touching Flask.

**Exercise arc:**
1. Watch browser requests in Developer Tools — see what an HTTP request looks like
2. Build a tiny HTTP server by hand (using Python's built-in `http.server`)
3. Write manual HTML responses — understand what the browser actually receives
4. Then introduce Flask as a tool that makes this easier

**Architecture:**
```
Browser
  ↓ (HTTP Request)
Server
  ↓ (SQL Query)
Database
  ↑ (Results)
Server
  ↑ (HTML Response)
Browser
```

**Then add Tailwind CSS** for the UI:
- Dashboard showing library stats
- Search page with results
- Book detail page
- Member management

---

## Part 8 — Security

**Principle:** Experience the vulnerability before learning the fix.

**Exercise arc:**
1. Store passwords in plaintext in the database
2. Open the SQLite file directly — read every password
3. Feel the risk of what just happened
4. Introduce bcrypt — one-way hashing
5. SQL injection — demonstrate how a malicious search query can destroy data
6. Sessions — how authentication state is maintained between requests
7. HTTPS — why unencrypted traffic can be read by anyone on the network

**Concepts:** authentication, authorization, sessions, SQL injection, bcrypt, HTTPS

---

## Part 9 — Networking

**Key experiment:**
- `library.elasticnode.com` works on Laptop A
- Same URL fails on Laptop B
- Both are on the same Wi-Fi

**Exercise arc:**
1. Compare DNS settings on both laptops
2. Understand that `library.elasticnode.com` is a private DNS record — it only
   exists on the Raspberry Pi's BIND server
3. Change Laptop B's DNS server to the Raspberry Pi
4. Observe that it now works

**Concepts:** IP addresses, DNS, subnet masks, routers, gateways,
private DNS vs public DNS vs authoritative DNS

**BIND setup on Raspberry Pi — local DNS records:**
- `library.elasticnode.com`
- `school.elasticnode.com`
- `git.elasticnode.com`

---

## Part 10 — Deployment

**Key distinction:** Running on a laptop ≠ running as a service.
A service runs 24/7, survives reboots, handles multiple users, recovers automatically.

**Full deployment stack:**
```
Browser
  ↓
DNS (Raspberry Pi — BIND)
  ↓
Nginx (reverse proxy)
  ↓
Flask (app server — systemd service)
  ↓
SQLite (database)
```

**Topics:**
- Nginx configuration as reverse proxy
- Running Flask as a systemd service (auto-restart, starts on boot)
- Cron jobs: daily backup of `library.db`, weekly usage report, monthly statistics
- Basic monitoring: knowing when the service has gone down

**Cron job principle:** Introduce only after a manual repetitive task has been
done enough times to feel annoying. The pain justifies automation.

---

## Part 11 — AI-Assisted Engineering

**Key principle:** AI can generate the code. The engineer must know if it is correct.

**What AI can generate:**
- Flask routes and views
- SQL queries and migrations
- Git commit messages
- Tailwind CSS layouts
- Test cases

**What engineers must still do:**
- Understand the architecture
- Identify security risks in generated code
- Design the data model
- Make trade-off decisions
- Review, test, and refactor AI output

**Exercise arc:**
1. Use AI to generate a feature for the library system
2. Review the output — find what is wrong, insecure, or poorly designed
3. Fix it
4. Explain why each fix was needed

**The question:** If AI wrote this code, how would you know it is correct?

---

## Library Project Evolution

| Version | What changes |
|---------|-------------|
| v1 | CLI + CSV (Mini Library, Part 0) |
| v2 | Git history and branching (Part 3) |
| v3 | Refactored into modules (Part 4) |
| v4 | 10,000+ real books from Open Library (Part 5) |
| v5 | SQLite replaces CSV (Part 6) |
| v6 | Flask web interface with Tailwind (Part 7) |
| v7 | Login and authentication (Part 8) |
| v8 | bcrypt passwords, SQL injection protection (Part 8) |
| v9 | Running on Raspberry Pi with DNS (Part 9) |
| v10 | Full deployment: Nginx + systemd + cron (Part 10) |
| v11 | AI-assisted feature development (Part 11) |

---

## GitHub Pages Technical Setup

**Live URL:** `https://manu.github.io/learn-by-doing.github.io`

**Repository:** `git@github.com:manu/learn-by-doing.github.io.git`

**Theme:** just-the-docs (via `remote_theme: just-the-docs/just-the-docs`)

**`docs/_config.yml` settings:**
```yaml
title: Engineering Through One Project
remote_theme: just-the-docs/just-the-docs
url: "https://manu.github.io"
baseurl: "/learn-by-doing.github.io"
plugins:
  - jekyll-remote-theme
  - jekyll-seo-tag
```

**Pages source:** `main` branch, `/docs` folder (configured in GitHub Settings → Pages)

**Navigation:** just-the-docs uses front matter to build the sidebar:
- Top-level sections: `nav_order`, `has_children: true`
- Child pages: `parent: Section Title`, `nav_order: N`

---

## What Is Built So Far

### Home page (`docs/index.md`)
- Introduction: software engineering is about solving problems, not writing Python
- Real-world examples: Zomato, hospitals, farms, traffic, fishing, translation
- The guiding question: "What problem was this technology invented to solve?"
- Curriculum table linking all 12 parts

### Part 0 — 8 complete exercises
0.1 Temperature Converter · 0.2 Age Calculator · 0.3 Fibonacci ·
0.4 Marks Analysis · 0.5 Student Records · 0.6 Book Catalog ·
0.8 Prime Checker · 0.26 Mini Library

### Part 1 — 1 exercise
1.1 Messy Folder (reorganize project, write README, audit variable names)

### Part 2 — 1 exercise
2.1 Global Variable Disaster (find bugs, understand scope, rewrite with parameters)

### Parts 3–11 — overview pages only (exercises not yet written)

### Glossary — 9 terms defined
### Architecture Reviews — review framework and milestone table

---

## What Is Still To Build

### Immediate (Parts 3–11 exercises)

Each part needs 3–8 exercises following the same template.
Priority order matches Amal's learning sequence.

**Part 3 — Git**
- 3.1 Version Confusion (exists, complete)
- 3.2 First commit — commit the Mini Library, write meaningful messages
- 3.3 Branches — add a feature on a branch, merge it
- 3.4 Issues — file a bug report, file a feature request
- 3.5 Pull Request — open a PR, review it, merge it

**Part 4 — Refactoring**
- 4.1 The 300-Line File — given a bloated library.py, identify the problems
- 4.2 Extract functions — break it apart
- 4.3 Split into modules — books.py, members.py, storage.py
- 4.4 Remove duplication — find repeated patterns

**Part 5 — Real Data**
- 5.1 Import 10,000 books from Open Library CSV
- 5.2 Measure performance (startup, search, memory)
- 5.3 Import 100,000 books — observe the difference

**Part 6 — SQL**
- 6.1 Why CSV hurts — articulate the specific failures
- 6.2 Design the schema — draw it before writing SQL
- 6.3 Create tables and migrate data
- 6.4 Search, join, filter with SQL
- 6.5 Add an index — measure the speed difference

**Part 7 — Web**
- 7.1 Watch a request in DevTools
- 7.2 Build a tiny HTTP server by hand
- 7.3 First Flask route
- 7.4 Book list page with Tailwind
- 7.5 Search form

**Part 8 — Security**
- 8.1 Plaintext password database — inspect it
- 8.2 Add bcrypt hashing
- 8.3 SQL injection demo — break your own database
- 8.4 Fix SQL injection with parameterized queries
- 8.5 Sessions and login flow

**Part 9 — Networking**
- 9.1 DNS Mystery (exists, complete)
- 9.2 Set up BIND on Raspberry Pi
- 9.3 Add local DNS records for elasticnode.com

**Part 10 — Deployment**
- 10.1 Run Flask on Raspberry Pi
- 10.2 Set up Nginx as reverse proxy
- 10.3 Run Flask as a systemd service
- 10.4 First automated backup (cron)
- 10.5 Weekly report cron job

**Part 11 — AI**
- 11.1 Review AI-generated code — find the flaws
- 11.2 Use AI to write a feature, then test it rigorously
- 11.3 Prompt engineering for code tasks

### Future improvements

- **Previous / Next navigation** on every exercise page
- **Mermaid architecture diagrams** embedded in part overview pages
- **Estimated effort** per exercise (e.g., "1 session", "2 sessions")
- **Acceptance criteria** — what "done" looks like for each exercise
- **Architecture Review pages** as actual content (not just a framework)
- **Open Library dataset** — download instructions and import scripts
- **GitHub Issue templates** in `.github/ISSUE_TEMPLATE/` for bug reports,
  feature requests, and refactoring tasks
- **Roadmap page** (`docs/roadmap.md`) showing the full 2-year arc visually

---

## Final Learning Goals

By the end of 2 years, Amal should be able to explain — in plain English,
to someone who does not write code — why each of these exists:

- Git
- SQL
- Indexes
- DNS
- Web servers
- The request-response model
- bcrypt
- Refactoring
- Cron jobs
- Web frameworks

And the answer to every one of them begins with the same words:
**"The problem was..."**
