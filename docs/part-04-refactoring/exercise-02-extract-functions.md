---
title: "4.2 Extract Functions"
parent: Refactoring
nav_order: 2
---

# Exercise 4.2 — Extract Functions

## The Story

After Exercise 4.1, you made one targeted fix. But the diagnosis revealed something bigger: the main loop of the library is doing everything itself. It reads input. It validates it. It searches. It displays. It saves. All of this is written inline, directly in the loop — hundreds of lines that flow into each other with no clear boundaries.

Here is the question that reveals the problem: **can you explain what the program does without reading the code?**

Try it. Cover the code. Describe what happens when the user picks "Add Book." You probably need to say things like: "well, it checks if the input is empty, then converts the year, then appends to the list, then writes to the file..." You are narrating the *code*. You are not describing the *idea*.

A well-structured program should be describable in terms of ideas — not code steps. "It validates the book details, then adds it to the collection, then saves the collection." Each of those phrases is a function waiting to exist.

## What to Do

### Part A — Find the ideas with no names

Read your main loop again. For every block of code that does something distinct, write a name for what it does — as if you were naming a function. Do not write any code. Just the names.

For example, you might write:
- "this part shows the menu"
- "this part gets the user's choice and validates it"
- "this part loads all books from the CSV"
- "this part checks if a book with this title already exists"

Write every name you find. These are the functions that need to exist.

### Part B — One extraction at a time

Start with the simplest idea you named — the one with no inputs and no outputs, something that only displays. Extract it into its own function.

After the extraction:
- Run the program. Every feature must work identically.
- Read the place where the code used to be. What is there now? Just a function call with a meaningful name.
- Can you understand what that section does now, without reading the function body?

If yes — the extraction worked. If you still need to read inside the function to understand the calling code — the function name is not good enough yet.

Extract the next idea. Verify. Repeat.

### Part C — Read the main loop after all extractions

When all extractions are done, read only the main loop — do not read any function bodies.

Ask yourself: can I understand the whole program's behaviour just from this? Can I follow every path — add book, search, delete, borrow — just by reading the function names?

If yes: the code is now readable at two levels of detail. The main loop is the high-level map. The individual functions are the detailed terrain. A reader can decide which level they need.

If no: a function name is not doing its job. Rename it until it is.

### Part D — The naming test

For each function you extracted, cover its body. Can you predict what it does from its name alone?

Ask a classmate or family member to read your function names aloud. Do they sound like English? Do they describe an action?

A function named `process()` fails this test. A function named `validate_year_input()` passes it.

## Before You Start — Think About This

1. You extract a chunk of code into a function. The function needs three pieces of data from the surrounding context. What does this tell you about the design of that chunk? What should you do about it?
2. After extraction, the total line count of your file will probably increase slightly. Why — and why is this not a problem?
3. Is there ever a reason NOT to extract a function? What situations make extraction make things worse rather than better?

## When You're Stuck

- Start with the easiest extraction: something that only produces output and needs no input. This builds confidence before tackling harder extractions.
- If an extracted function needs data from the surrounding scope, that data becomes a parameter. Ask: what does this function need to know to do its job?
- If an extracted function produces a result the caller needs, it returns that result. Ask: what does this function hand back?
- A function is correctly extracted when you can delete the original inline code, call the function instead, and the program is identical.

## Once It Works — Go Further

1. After extraction, pick one function and test it directly — call it yourself with specific inputs and check the output, without running the whole program. This is the beginning of unit testing: testing one piece in isolation. Which functions are easiest to test this way, and why?
2. You probably found some extractions were easy and some were hard. What made the hard ones hard? Were they tangled with too many other things? That tanglement itself is a design problem worth understanding.
