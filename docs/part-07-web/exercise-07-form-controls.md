---
title: "7.7 Form Controls"
parent: Web Architecture
nav_order: 7
---

# Exercise 7.7 — Form Controls

## The Story

The librarian sits down with you to review the "Add Book" form. Right now it has three text boxes: title, author, year. She has a list of changes:

> "Genre must be one of our fixed categories — Fiction, Non-Fiction, Reference, Biography, Science, History, Children. Right now people type anything and the database is a mess. Half our books say 'Sci-Fi', half say 'Science Fiction', one says 'SciFi' with no space."

> "Description should be multiple lines. A title is short, a description is long. Why do they have the same input?"

> "Available should be a tick box — either the book is available to borrow or it isn't."

> "Format: Paperback, Hardcover, eBook, or Audiobook. Only one at a time. A book is not both a Paperback and an eBook."

> "Target audience: Children, Young Adult, Adult. A book can be for more than one audience. 'The Alchemist' is for Young Adults and Adults."

Each of these requirements calls for a different HTML input control. A plain text box handles exactly none of them correctly.

## The Controls

Study each control and understand what problem it solves:

**Text input** — `<input type="text">` — Free text, one line. Use when any value is valid and the user knows what to type.

**Textarea** — `<textarea>` — Free text, multiple lines. Use when the value is long or naturally spans lines (descriptions, notes, addresses).

**Select (dropdown)** — `<select>` with `<option>` — Choose exactly one from a fixed list. Use when there are many options and only one is valid.

**Radio buttons** — `<input type="radio">` — Choose exactly one from a small fixed list. Use when there are 2–5 options and you want all choices visible at once.

**Checkbox** — `<input type="checkbox">` — Toggle a single yes/no value. Use for binary choices (available/unavailable, active/inactive).

**Select multiple** — `<select multiple>` — Choose one or more from a fixed list. Use when multiple selections are valid.

**Checkbox group** — Multiple `<input type="checkbox">` with the same `name` — Choose one or more from a small visible list. An alternative to select multiple when you want the options always visible.

## What to Do

### Part A — Match control to requirement

Before writing any HTML, match each library field to the correct control. Write your answer and justify it in one sentence:

| Field | Options / Constraint | Which control? Why? |
|-------|---------------------|---------------------|
| Title | Any text, short | ? |
| Author | Any text, short | ? |
| Year | A number | ? |
| Description | Any text, long | ? |
| Genre | Fiction, Non-Fiction, Reference, Biography, Science, History, Children — pick one | ? |
| Format | Paperback, Hardcover, eBook, Audiobook — pick one | ? |
| Available | Yes or No | ? |
| Target Audience | Children, Young Adult, Adult — pick one or more | ? |

Compare your answers with the list above. Where do you agree? Where did you make a different choice — and why might your choice also be valid?

### Part B — Build the form

Create `templates/add_book.html`. Build the full "Add Book" form using the correct control for each field. The form should:
- Use `method="POST"` and `action="/add"`
- Have a clear label for every control
- Group related fields visually (use Tailwind to style it)
- Have a Submit button labeled "Add to Library"

### Part C — Read the data in Flask

Update the `/add` route in Flask to read every field from `request.form`. Pay attention to these differences:

- A checkbox sends its value only when checked. If unchecked, the key is absent from `request.form`. How do you handle that?
- A select multiple sends multiple values under the same key. `request.form.get("audience")` only gives you the first one. How do you get all of them?
- A radio button group sends the value of whichever option is selected.

Print all the received values to the console first. Confirm every field arrives correctly before writing to the database.

### Part D — Validate the input

What happens if someone submits the form with an empty title? What if year is left blank? What if genre is not in your list?

Add validation in Flask before saving to the database:
- Title must not be empty
- Year must be a number
- Genre must be one of the allowed values

If validation fails, send the user back to the form with an error message. The form should re-populate the fields they already filled in so they do not have to start over.

## Topics You Will Learn

- `<input type="text">`, `<input type="number">`, `<input type="checkbox">`, `<input type="radio">`
- `<textarea>` and when to use it instead of a text input
- `<select>` for single-choice dropdowns
- `<select multiple>` and checkbox groups for multi-choice
- How each control sends its data to the server (and what happens when it sends nothing)
- `request.form.getlist("name")` to receive multiple values for the same key
- Server-side form validation and re-populating form fields after a validation error

## Before You Start — Think About This

1. A text input allows "Sci-Fi", "Science Fiction", "scifi", and "SCIENCE FICTION" to all enter the database. A dropdown allows only fixed options. What does this tell you about where data quality is enforced — in the interface, or in the database, or both?
2. Radio buttons show all options at once. A dropdown hides them until clicked. If you have 20 genre options, which is better and why?
3. A checkbox sends nothing when unchecked. A radio button always sends one value (whichever is selected). How does this difference affect how you write the Flask code to read each one?

## When You're Stuck

- Checkbox: `available = "available" in request.form` — checks whether the key is present at all.
- Select multiple / checkbox group: `audiences = request.form.getlist("audience")` — returns a list.
- To re-populate a dropdown after validation failure, you need to pass the submitted value back to the template and mark the right `<option>` as `selected`. Think about how you would do that.
- For radio buttons, add `checked` to the `<input>` element of the previously selected option when re-rendering after a validation error.

## Once It Works — Go Further

1. Add an `<input type="date">` for a "Date Added" field. What does Flask receive? What format is the date in? How would you store it in SQLite?
2. Add a file upload field (`<input type="file">`) that allows the librarian to upload a cover image for a book. This requires `enctype="multipart/form-data"` on the form and `request.files` in Flask. What does Flask do with the uploaded file?
3. Look at how the search form from Exercise 7.5 uses `<input type="text">`. Could it benefit from `<input type="search">` instead? Look up the difference.
