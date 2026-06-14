---
title: "3.4 GitHub Issues"
parent: Git and History
nav_order: 4
---

# Exercise 3.4 — GitHub Issues

## The Story

Your library program has a bug: if the user enters a year that is not a number (for example, they type `"unknown"` instead of `1984`), the program crashes.

You found this bug on a Tuesday evening. By Thursday morning you have forgotten about it. By next week it no longer exists in your memory at all — until a user hits it and the program crashes in front of them.

This is why engineers use issue trackers. An issue is a recorded problem, feature request, or improvement — with a title, a description, and enough information for anyone (including future-you) to understand and act on it.

GitHub Issues is the issue tracker built into every GitHub repository.

## What to Do

### Step 1 — Push your library to GitHub

If you have not already done this, create a repository on GitHub and push your local library project:

```
git remote add origin git@github.com:yourusername/mini-library.git
git push -u origin main
```

### Step 2 — File a bug report

Go to your repository on GitHub. Click **Issues** → **New issue**.

Write a bug report for the year-input crash. A good bug report has:

- **Title**: Short, specific. "Program crashes when year is not a number."
- **Steps to reproduce**: Exactly what to do to see the bug.
- **Expected behaviour**: What *should* happen.
- **Actual behaviour**: What *does* happen (include the error message).
- **Environment**: Python version, OS.

### Step 3 — File a feature request

File a second issue — a feature request. Choose something you genuinely want to add to the library. Write:

- **Title**: "Add ability to delete a book"
- **Why**: What problem does this solve? Who would use it?
- **Proposed behaviour**: What would the user experience look like?

### Step 4 — Fix the bug on a branch

Create a branch: `git checkout -b fix-year-input-crash`

Fix the bug. The fix should handle non-numeric input gracefully — print an error message and ask again, rather than crashing.

Commit the fix with a message that references the issue number:
```
git commit -m "Handle non-numeric year input gracefully — fixes #1"
```

Push and open a Pull Request on GitHub. In the PR description, write what you changed and why.

## What to Observe

After merging the PR, go back to the Issues tab. Issue #1 should now be automatically closed (GitHub closes issues referenced in merged PRs with "fixes #N"). The history shows who fixed what, when, and why.

This is the complete workflow: Issue → Branch → Commit → PR → Merge → Issue closed.

## Topics You Will Learn

- How to write a useful bug report
- How to write a useful feature request
- Linking commits and PRs to issues with `fixes #N`
- The complete GitHub workflow: issue → branch → PR → merge

## Before You Start — Think About This

1. What is the difference between a bug report and a complaint? ("This is broken" vs "When I do X, Y happens instead of Z.")
2. A feature request that says "make it better" is not actionable. What makes a feature request useful enough to act on?
3. Why should you reference an issue number in a commit message? Who benefits from that link six months later?

## When You're Stuck

- To catch invalid input, use a `try/except` block around the `int()` conversion.
- If your repo is private, issues are still available — they are not tied to visibility.
- You can label issues ("bug", "enhancement", "question") using the Labels sidebar in GitHub. Labels help triage a long list of issues.

## Once It Works — Go Further

1. Add a label system to your issues — create labels called `bug`, `enhancement`, and `good first issue`. Apply appropriate labels to both issues.
2. Write a third issue for a refactoring task: "Split library.py into separate modules." Describe which modules you would create and what each one would contain.
