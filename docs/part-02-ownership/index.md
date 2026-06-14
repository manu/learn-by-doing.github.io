---
title: Ownership and Responsibility
nav_order: 4
has_children: true
---

# Ownership & Responsibility

Who owns the data? Who is allowed to change it?

These are not just software questions — they are engineering discipline questions. This section is inspired by how Rust thinks about memory ownership, applied to how we design Python programs.

## Key Concepts

- Avoid global variables — pass data in, return it out
- Explicit data flow — trace where every value comes from and goes
- References vs copies — know whether a function modifies the original
- Ownership — one responsible party per piece of data
- Pure functions vs side effects — separate calculation from action
- Single Source of Truth — data lives in exactly one authoritative place

## Exercises

- [2.1 Global Variable Disaster](exercise-01-global-variable-disaster.md)
- [2.2 Mutable and Immutable](exercise-02-mutable-immutable.md)
- [2.3 Trace the Data](exercise-03-trace-the-data.md)
- [2.4 Who Owns This?](exercise-04-who-owns-this.md)
- [2.5 Pure Functions and Side Effects](exercise-05-pure-functions.md)
- [2.6 Single Source of Truth](exercise-06-single-source-of-truth.md)