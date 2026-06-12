---
title: "0.1 Temperature Converter"
parent: Python Recall Bootcamp
nav_order: 1
---

# Exercise 0.1 — Temperature Converter

## The Story

A school library gets its weather data from an American website. The data comes in Fahrenheit. But students in India understand Celsius. Someone needs to build a converter.

This is your first program. It is small. That is intentional — the point is to get one program running cleanly before making anything bigger.

## What to Build

Your program should ask for a temperature in Fahrenheit and print the result in Celsius.

```
Enter temperature in Fahrenheit: 98.6
That is 37.0 degrees Celsius.
```

Try it with a few values you already know:
- 32°F → 0°C (freezing point of water)
- 212°F → 100°C (boiling point of water)
- 98.6°F → 37°C (normal human body temperature)

## Topics You Will Need

- `input()` — to read something the user types
- `float()` — to convert text into a number with decimals
- Variables — to store values and reuse them
- Arithmetic operators — `+`, `-`, `*`, `/`
- `print()` — to show the result

## Before You Start — Think About This

1. When you type something in `input()`, Python receives it as text. What do you need to do before you can do arithmetic on it?
2. The formula is: subtract 32, then multiply by 5, then divide by 9. Does the order matter? What happens if you divide first?
3. How many decimal places should the answer show? Is `37.000000000001` a good output?

## When You're Stuck

- Look up how `float()` works and why `int()` would not be the right choice here.
- Python follows the standard order of operations (BODMAS). Use brackets to control the order.
- To control decimal places in the output, look up Python's `round()` function.

## Once It Works — Go Further

1. Make it work in both directions — ask the user whether they want F→C or C→F, then do the right conversion.
2. Add a check: if the temperature entered is below −273.15°C (absolute zero), print a message saying that temperature is physically impossible.
3. Print a small table showing conversions for 0°F, 32°F, 98.6°F, 212°F all at once.
