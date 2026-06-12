---
title: "11.1 Review AI-Generated Code"
parent: AI-Assisted Engineering
nav_order: 1
---

# Exercise 11.1 — Review AI-Generated Code

## The Story

An AI assistant generated a Flask route for adding a new book to the library. The code runs. The tests pass. The product manager is happy.

You are the engineer. Your job is to review it before it goes to production.

## The Code to Review

```python
@app.route('/add-book', methods=['GET', 'POST'])
def add_book():
    if request.method == 'POST':
        title = request.form['title']
        author = request.form['author']
        year = request.form['year']
        
        conn = sqlite3.connect('library.db')
        c = conn.cursor()
        c.execute("INSERT INTO books VALUES (null, '" + title + "', '" + author + "', " + year + ")")
        conn.commit()
        conn.close()
        
        return redirect('/')
    
    return render_template('add_book.html')
```

## What to Do

### Step 1 — Read it carefully

Read the code three times before writing anything down. Understand what it does.

### Step 2 — Find the problems

There are at least four distinct problems in this code. Find them. For each one, write:

1. What the problem is (describe it precisely)
2. What could go wrong because of it (the consequence)
3. How you would fix it

Do not look up the answers. Work through the code yourself first.

### Step 3 — Classify each problem

After finding the problems, classify each one:
- **Security vulnerability** — an attacker could exploit this
- **Reliability issue** — the code will fail under normal circumstances
- **Maintainability problem** — the code works but will cause pain later
- **Missing feature** — something the code should do but does not

### Step 4 — Write the fixed version

Rewrite the route so that all the problems are fixed. The functionality should be identical — a POST request adds a book, a GET request shows the form — but the implementation should be correct.

### Step 5 — Reflect on the review process

After fixing the code, answer:
1. Which problem was most dangerous?
2. Which problem would have been hardest to find without a deliberate review?
3. If you had just run the code and seen it work, would you have caught any of these problems?

## Topics You Will Learn

- Code review as an engineering discipline
- Security vulnerability identification (SQL injection, missing authentication)
- Input validation — what to check, what to reject
- Error handling — what happens when something unexpected arrives
- Why "it works" is not the same as "it is correct"

## Before You Start — Think About This

1. AI generates code that is syntactically correct and often logically reasonable. What categories of problems is it likely to miss? (Security? Edge cases? Context-specific requirements?)
2. This code has a SQL injection vulnerability. You have seen this before — in Part 8. Does recognising a known vulnerability pattern feel different from finding a new type of problem?
3. The code works for a valid, honest input. What are all the ways a less-than-honest input could be provided? What is the set of things you need to protect against?

## Once It Works — Go Further

1. Ask an AI assistant to generate a different Flask feature — for example, a loan tracking endpoint. Then apply the same review process. How many problems do you find this time?
2. Write a personal checklist of things you look for in every code review. Include at least: SQL injection, authentication check, input validation, error handling. Add items as you find patterns across multiple reviews.
