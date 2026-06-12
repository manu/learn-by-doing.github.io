---
title: "4.4 Remove Duplication"
parent: Refactoring
nav_order: 4
---

# Exercise 4.4 — Remove Duplication

## The Story

There is a principle in software engineering called **DRY — Don't Repeat Yourself**. It states that every piece of knowledge should have a single, unambiguous representation in the system.

When the same logic exists in two places, it will eventually diverge. A bug is fixed in one place but not the other. A requirement changes and one copy is updated while the other is forgotten. Now the system behaves differently in two seemingly identical situations — and nobody knows why.

Duplication is not always obvious. Sometimes it is two functions that do nearly the same thing. Sometimes it is two blocks of code that follow the same structure with different values. Sometimes it is a condition (`if year > 2000`) that appears in five different places — and when the rule changes to `if year > 1990`, you have to find all five.

## What to Do

### Step 1 — Find the duplication

Read through your library modules. Look for:

1. **Obvious duplication**: Two functions that do the same thing with slightly different variable names
2. **Structural duplication**: Two sections of code that follow the same pattern but operate on different data
3. **Data duplication**: A value (like a year threshold or a filename) that is written out in multiple places

Write down each instance before fixing anything.

### Step 2 — Deduplicate one instance

Start with the most obvious case. Common fixes:

- **Two functions that do the same thing** → delete one, update all callers to use the other
- **Two blocks with the same structure** → extract one function with a parameter for what differs
- **A repeated value** → define it as a constant at the top of the relevant module and reference it everywhere

### Step 3 — The test of duplication removal

After deduplicating, make one change to the single remaining implementation. Verify that the change is reflected everywhere that used to have a copy. If it is — the duplication is gone. If you still need to change something in another place — you did not find all the copies.

## Topics You Will Learn

- The DRY principle and why it exists
- How to identify non-obvious duplication
- Constants — named values that prevent magic numbers from proliferating
- The trade-off: too much deduplication can create over-engineered abstractions

## Before You Start — Think About This

1. Two functions that do the same thing but have different names — that is duplication. But what if they do 90% the same thing and 10% differently? Is extracting a shared function the right move, or does it make the code harder to read?
2. The opposite of DRY is sometimes called WET — "Write Everything Twice" or "We Enjoy Typing". When might duplication actually be the right choice?
3. If you have `if status == "borrowed":` in five different places and the requirement changes to also include `"overdue"` as a borrowed state — how do you make that change safely if the condition is duplicated? How does this change if the condition is in one place?

## When You're Stuck

- If two functions are almost identical, copy one and delete the parts that are the same. What remains is the part that differs — that becomes the parameter.
- Constants go at the top of the module, in UPPERCASE: `LIBRARY_FILE = "library.csv"`. Every place that previously had the string `"library.csv"` can now reference `LIBRARY_FILE`.
- Be careful of over-deduplication: if you extract a shared function that is so general it is hard to understand what it does, you have made the code harder to read in exchange for removing the duplication. The cure should not be worse than the disease.

## Once It Works — Go Further

1. Read about the **Rule of Three** in software engineering: duplication is acceptable once, worth noting the second time, and should be eliminated the third time. Do you agree with this rule? Is there a simpler version of it that you would apply?
2. Now that your code is clean — modular, well-named, free of duplication — write a short architecture note describing how the Mini Library works. Keep it to half a page. This is what engineers call a design document, and it becomes more valuable as the project grows.
