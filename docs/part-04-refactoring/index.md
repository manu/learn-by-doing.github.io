---
title: Refactoring
nav_order: 6
has_children: true
---

# Refactoring

Refactoring means improving the design of code without changing what it does.

The program behaves identically before and after. But it becomes easier to read, easier to change, and easier to extend.

## Key Concepts

- Diagnosing before fixing — read and list problems before changing anything
- Naming as design — a hard-to-name thing is almost always a design problem
- Extract functions — give unnamed ideas a name and a boundary
- Separate concerns — each file has one reason to change
- Remove duplication — every piece of knowledge in exactly one place
- Code smells — patterns that signal a problem worth investigating
- Architecture review — articulating what changed and why it matters

## The Questions to Ask

- What is difficult to understand?
- What would be hard to change?
- What would break if I changed this one thing?
- If I cannot name this — what does that tell me about its design?

## Exercises

- [4.1 The 300-Line File](exercise-01-300-line-file.md)
- [4.2 Extract Functions](exercise-02-extract-functions.md)
- [4.3 Split into Modules](exercise-03-split-modules.md)
- [4.4 Remove Duplication](exercise-04-remove-duplication.md)
- [4.5 Code Smells](exercise-05-code-smells.md)
- [4.6 Naming as Design](exercise-06-naming-as-design.md)
- [4.7 Before and After](exercise-07-before-and-after.md)