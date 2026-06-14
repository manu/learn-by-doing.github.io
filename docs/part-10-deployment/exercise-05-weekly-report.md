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

### Part A — Write the queries first

Before writing any Python, write and test the SQL queries in DB Browser. Verify each one returns correct results:

1. How many loans were created in the last 7 days?
2. What are the top 5 most borrowed books in the last 7 days?
3. Which 3 members borrowed the most in the last 7 days?
4. Which books are currently overdue — borrowed more than 14 days ago and not yet returned?
5. Total books, total members, total active loans right now

For the "last 7 days" queries, think carefully: if the report runs on Monday, does "last 7 days" mean the 7 days before today, or the calendar week from Monday to Sunday? Which is more useful to the librarian?

### Part B — Write the report script

Create `generate_report.py`. It should run all five queries and produce a report file in a `reports/` folder. The filename should include the date.

The output should look like something a librarian could read or print — not a technical debug dump. Design the format on paper first: what sections, what headings, how the numbers should be presented.

Run the script manually. Open the report file. Read it as if you were the librarian. Is it clear? Is anything missing or confusing?

### Part C — Schedule with cron

Add a cron entry to generate the report every Monday at 7am. The librarian should find a new report ready when she arrives.

Test it without waiting for Monday: set the schedule to run one minute from now, verify the report is generated, then set it back to Monday mornings.

### Part D — Verify correctness

Cross-check the numbers in the report against the database in DB Browser. Pick one number from the report — say, "overdue books: 3" — and manually verify it by running the query yourself. Do the numbers match?

A report with wrong numbers is worse than no report — the librarian will act on incorrect information.

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
