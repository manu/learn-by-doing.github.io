---
title: "5.3 Why Is It Slow?"
parent: Real Data
nav_order: 3
---

# Exercise 5.3 — Why Is It Slow?

## The Story

You have the measurements. You know the library is slow. But the librarian does not want measurements — she wants to understand.

"Is it the computer? Is it Python? Is it my internet connection?"

"No," you say. "It is the design."

"What do you mean?"

You pause. You know it is slow. You can prove it with numbers. But can you explain *why*? Can you describe, to someone who has never seen the code, exactly what the computer is doing that makes it slow?

Understanding *why* something is slow — not just *that* it is slow — is the difference between being able to fix it and blindly trying things.

## What to Do

### Part A — Trace one search by hand

Forget code for a moment. Imagine the library's book list as a physical stack of 10,000 index cards on a table, one card per book, in no particular order.

A student walks up and asks: "Do you have any books about photography?"

You pick up the first card. Does it mention photography? No. You put it aside. You pick up the second card. No. Third. No. You continue, card by card, through all 10,000.

That is exactly what your `search_books()` function does.

Now answer these questions in writing:
1. In the worst case (no books match the query), how many cards did you check?
2. If the stack had 100,000 cards instead of 10,000, how many would you check in the worst case?
3. If each card-check takes 0.001 milliseconds, how long does a search take with 10,000 books? With 100,000?
4. Does the time grow in proportion to the number of cards?

### Part B — What a smarter system would do

Imagine the same 10,000 cards, but now they are sorted alphabetically by title and arranged in labelled sections: A–D, E–H, I–L, and so on.

A student asks for books about "Photography."

You go straight to the P section. You look at roughly 1,000 cards instead of 10,000. Still slow — but better.

Now imagine the cards are organised by topic as well, with a separate index card at the front that lists every topic and the card numbers that match. To find "Photography", you look up one card in the index, get the numbers, and retrieve those specific cards directly.

You found your answer without checking thousands of cards.

Answer these questions:
1. With the topic index, how many cards did you check to answer the photography query?
2. Why is the index much faster than checking all cards?
3. To build the index, someone had to go through all 10,000 cards once and record each topic. Was that upfront work worth it? Under what conditions?

This is how a database index works. You will build one in Part 6.

### Part C — Try to make it faster yourself

Without changing the architecture (still a list, still a CSV), try at least two approaches to make the search faster and measure whether they help:

**Approach 1:** Sort the book list when it loads. Does a sorted list help with a partial-title search?

**Approach 2:** Stop searching after finding the first 20 matches instead of scanning the full list. Does early exit help?

For each approach: measure the search time before and after. Write down how much improvement you got, if any.

Then answer: is the improvement enough? At 100,000 books, does any of your optimisation make the library fast enough to use comfortably?

### Part D — State what you need

Based on Parts A–C, write a paragraph describing what a better storage system would need to do. Write it in plain English, not in technical terms. Something like:

*"The storage system needs to be able to find all books matching a query without checking every book. It needs to be able to do this even for a million books. It needs to handle multiple people searching at the same time. It needs to store data in a way that survives if the program crashes..."*

Write your own version. This paragraph is your specification. It is the problem statement that Part 6 will solve.

## Before You Start — Think About This

1. The sort-and-search approach works well for exact matches. Why does it not help much for *partial* title searches (where you are looking for any book whose title *contains* a word)?
2. A database can answer "find all books by authors whose last name starts with M" without checking every book. How would a physical index card system solve this problem? How many different indexes would a real library need?
3. The current library loads all books into memory on startup. A database does not — it keeps data on disk and fetches only what is needed. Why does this matter when the dataset grows to 10 million books?

## When You're Stuck

- For Part C, measure carefully: run the same query before and after your change, with the same dataset size. A fair comparison needs identical conditions.
- The question is not "can I make it faster?" — you almost certainly can, a little. The question is "is any amount of optimisation enough?" The answer will lead you to Part 6.
- If a thought occurs to you like "what if I built a dictionary indexed by title?" — write it down. You are independently discovering the concept of an index. That thinking is exactly right.

## Once It Works — Go Further

1. You traced one search by hand and counted the steps. Now trace a *startup* (loading the CSV) the same way. How many operations does startup require? How does that scale with data size?
2. Your paragraph from Part D is the motivation for everything in Part 6. Keep it. After completing Part 6, come back and check: did SQL solve everything you listed?
