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

### Part A — Read it completely first

Read the code three times without writing anything. Understand what it does and what it is supposed to do.

Only after you understand the intent should you start looking for problems.

### Part B — Find the problems

There are at least four distinct problems in this code. Find them all before moving on. For each one, write:
- What the problem is (be specific about which line and what exactly is wrong)
- What could go wrong as a result (what an attacker could do, or how the system could fail)
- How you would fix it

Work through the code yourself. Do not search for the answers first.

### Part C — Classify each problem

After finding the problems, classify each one:
- **Security vulnerability** — an attacker could exploit this
- **Reliability issue** — the code will fail under normal or unexpected circumstances
- **Maintainability problem** — the code works but will cause problems as the system grows
- **Missing feature** — something the code should do but does not

### Part D — Write the corrected version

Rewrite the route so all the problems are fixed. The functionality must be identical — a POST request adds a book, a GET request shows the form — but the implementation must be correct.

### Part E — Reflect

After writing the fix, answer these questions:
1. Which problem was most dangerous?
2. Which problem would have been hardest to find without a careful review?
3. The code ran without errors. Someone tested it with a valid title and author and it worked. Would they have caught any of these problems during testing?
4. What does this tell you about the difference between "it works" and "it is correct"?

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
