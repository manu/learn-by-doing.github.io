---
title: "0.5 Student Records"
parent: Python Recall Bootcamp
nav_order: 5
---

# Exercise 0.5 — Student Records

## The Story

The library keeps a record of its members. Each member has a name, a member ID, and the number of books currently borrowed. The librarian needs to be able to:

1. See all members at once
2. Look up a specific member by name and see their details

In the previous exercise, you used two separate lists (one for names, one for scores) and kept track of positions. That works — but it gets fragile when each person has three or four pieces of information. There is a better way: *dictionaries*.

A dictionary groups all the information about one person into a single unit. This exercise teaches you to think in structured data — the same thinking you will use when you design databases later.

## What to Build

Start with a fixed list of 4 or 5 members already in the program (you do not need to enter them through `input()` for now). Then build a search.

```
--- Library Members ---
ID: 1001 | Name: Amal       | Books borrowed: 2
ID: 1002 | Name: Priya      | Books borrowed: 0
ID: 1003 | Name: Rohan      | Books borrowed: 3
ID: 1004 | Name: Fatima     | Books borrowed: 1
ID: 1005 | Name: Arjun      | Books borrowed: 0

Search by name (or press Enter to quit): Rohan

Member found:
  Name   : Rohan
  ID     : 1003
  Borrowed: 3 books
```

If the name is not found:

```
Search by name (or press Enter to quit): Kiran
No member found with that name.
```

## Topics You Will Need

- Dictionaries — `{"key": value, "key": value}` — to represent one member
- Lists of dictionaries — to hold all members
- `for` loop — to display all members and to search through them
- `while` loop — to keep the search running until the user presses Enter
- String comparison — to match the search input against names

## Before You Start — Think About This

1. A dictionary for one member might look like `{"name": "Amal", "id": 1001, "borrowed": 2}`. What are the *keys*? What are the *values*? How would you access just the name from this dictionary?
2. A list of dictionaries is just a list where each element is a dictionary. How is that different from a list of numbers?
3. When searching, you need to go through every member and check if the name matches. What loop would you use? What happens when you find a match — should you keep looking?
4. What should happen if the user searches and you find a match mid-loop? How do you stop the loop and remember that you found something?

## When You're Stuck

- Access a value in a dictionary with `my_dict["key"]`. For example, `member["name"]` gives you the name.
- To loop through a list of dictionaries: `for member in members:` — then inside the loop, `member` is one dictionary at a time.
- Use a variable like `found = False` before the loop. Set it to `True` when you find a match. After the loop, check `found` to decide what to print.
- To check if the user pressed Enter without typing anything: `if search == "":`

## Once It Works — Go Further

1. Add a feature to let the librarian add a new member through `input()`. Append the new member dictionary to the list.
2. Make the search case-insensitive — searching for "amal" should find "Amal". Look up `.lower()`.
3. Add a feature to update the `borrowed` count — ask for a member's name and whether they are borrowing (+1) or returning (-1) a book.
