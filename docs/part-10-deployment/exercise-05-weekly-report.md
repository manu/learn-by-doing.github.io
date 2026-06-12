---
title: "10.5 Weekly Report"
parent: Deployment
nav_order: 5
---

# Exercise 10.5 — Weekly Report

## The Story

The librarian wants to receive a weekly summary every Monday morning: how many books were borrowed last week, which books were most popular, which members borrowed the most, and how many books are currently overdue.

Before cron, this would require the librarian to remember to run a report manually every Monday. With cron, the report generates itself and could be printed or emailed automatically.

This exercise combines SQL queries, Python, shell scripting, and cron scheduling — all the tools from Part 6 and Part 10 working together.

## What to Do

### Step 1 — Write the report queries

Write the SQL queries that produce the weekly statistics. Run them in DB Browser first to verify the results:

1. Total loans in the last 7 days
2. Top 5 most borrowed books in the last 7 days
3. Top 3 members by loans in the last 7 days
4. Books currently overdue (borrowed > 14 days ago, not returned)
5. Total books in the library, total members, total active loans

### Step 2 — Write the report script

Create `generate_report.py`. This script should:
1. Connect to `library.db`
2. Run each query
3. Format the results as a readable text report
4. Write the report to a file: `reports/weekly-report-YYYY-MM-DD.txt`

The report should look like a document someone could print and read, not a debug dump.

```
=== Library Weekly Report ===
Week ending: 2026-06-12

ACTIVITY
--------
Books borrowed this week: 23
Books returned this week: 19
Currently on loan: 47
Overdue books: 3

MOST POPULAR THIS WEEK
----------------------
1. Sapiens — 4 loans
2. 1984 — 3 loans
3. The Alchemist — 2 loans

OVERDUE BOOKS
-------------
• "The Kite Runner" — borrowed by Priya (18 days ago)
• "Dune" — borrowed by Arjun (16 days ago)
...
```

### Step 3 — Schedule the report with cron

Add a cron entry to generate the report every Monday at 7am:
```
0 7 * * 1 python3 /home/pi/library-project/generate_report.py
```

`* * 1` means day-of-week = 1 (Monday).

### Step 4 — Verify the report

Run the script manually. Open the generated report file. Verify the numbers are correct by cross-checking against the database.

## Topics You Will Need

- SQL queries with `WHERE`, `GROUP BY`, `ORDER BY`, `LIMIT`, date comparisons
- Python: connecting to SQLite, running queries, formatting output
- Python: writing to a file, date formatting with `datetime`
- Cron: day-of-week field (0 = Sunday, 1 = Monday, ... 6 = Saturday)
- Shell: creating a directory if it does not exist (`mkdir -p reports/`)

## Before You Start — Think About This

1. The report covers "the last 7 days." If the script runs on Monday at 7am, what is the correct date range? Is it "the 7 days before today" or "last Monday to last Sunday"? Which is more useful to a librarian?
2. What happens if the report script crashes partway through? A partial report is written to the file. How do you make the script atomic — either the complete report is written, or nothing is?
3. The report is useful even without email — a librarian can check the `reports/` folder. But emailing it automatically would be more convenient. What would you need to set up to send the report by email?

## When You're Stuck

- `from datetime import datetime, timedelta` gives you date arithmetic. `datetime.now() - timedelta(days=7)` is one week ago.
- To format a date for SQL comparison: `date_str = (datetime.now() - timedelta(days=7)).strftime("%Y-%m-%d")`
- Build the report as a list of strings, then join them and write once at the end: `f.write("\n".join(lines))`. This is more robust than writing line by line.

## Once It Works — Go Further

1. Look up the `smtplib` Python module. Modify the script to send the report as a plain-text email after generating it. This is the complete monitoring pipeline: data → analysis → report → notification.
2. Add a chart to the report: a simple ASCII bar chart showing loans per day for the last week. For example: `Mon ████████ 8` / `Tue █████ 5`. Generate it purely with Python string operations.
