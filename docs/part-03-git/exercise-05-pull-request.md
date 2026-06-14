---
title: "3.5 Pull Request"
parent: Git and History
nav_order: 5
---

# Exercise 3.5 — Pull Request

## The Story

In a professional engineering team, no code goes directly into the main branch. Every change is proposed as a *pull request* — a formal request to pull a branch's changes into main. Before it is merged, at least one other engineer reviews it.

The review is not just about finding bugs. It is about asking questions like:
- Does this do what the issue asked for?
- Is there a simpler way?
- Will this break anything else?
- Will I understand this in six months?

Even when working alone, practising the PR workflow builds the discipline of *explaining your changes to another person* — which forces clearer thinking.

## What to Do

### Step 1 — Choose a feature to add

Pick the feature request issue you filed in Exercise 3.4 (or file a new one now). Something small but complete — for example: "Add ability to delete a book by title."

### Step 2 — Build it on a branch

```
git checkout -b feature-delete-book
```

Implement the feature. Make at least two commits as you work.

### Step 3 — Open the Pull Request

Push your branch to GitHub:
```
git push -u origin feature-delete-book
```

On GitHub, click **Compare & pull request**. Write a PR description that answers:

1. **What does this PR do?** — One sentence.
2. **Why?** — Which issue does it resolve? (Use `closes #N`)
3. **How?** — A brief description of the approach. Not a line-by-line explanation — the diff is visible. Explain the *decision*, not the mechanics.
4. **How to test it** — The exact steps to verify the feature works.

### Step 4 — Review your own PR

Read through the diff on GitHub as if you are a reviewer who did not write the code. Comment on at least two things — questions, concerns, or things you would do differently. Leave these as PR comments.

Then respond to your own comments — either explaining why you made the choice, or making a change based on the review.

### Step 5 — Merge

Merge the PR. Delete the branch. Confirm the issue is closed.

## What to Observe

The merged PR is now a permanent part of the repository's history. Go to the commit history — you will see a "Merge pull request #N" commit. Anyone who looks at this history in a year will be able to understand what changed, why, and what discussion happened before it was accepted.

Compare this to the alternative: a direct commit on main with the message `"added delete feature"`.

## Topics You Will Learn

- The full PR lifecycle: branch → push → PR → review → merge → delete branch
- How to write a PR description that is useful to a reviewer
- How code review works and why it matters
- The relationship between issues, branches, PRs, and commits

## Before You Start — Think About This

1. What is the purpose of code review? Is it primarily to find bugs, or does it serve other purposes?
2. Why should the PR description explain the *decision* and not the *mechanics*? (The diff shows what changed — so what does the description add?)
3. In a team, who should be allowed to merge a PR? Should the author of the code be allowed to merge their own PR without any review?

## When You're Stuck

- A good PR is small enough to review in under 30 minutes. If your PR is huge, it is too big — split it into smaller ones.
- If you push more commits to the branch after opening the PR, they are automatically added to the PR. You do not need to close and reopen it.
- "Squash and merge" combines all your branch commits into one commit on main. "Merge commit" keeps all the commits. Ask yourself which tells a cleaner story in the long run.

## Once It Works — Go Further

1. Over the next five exercises, practice the full workflow for every change you make: issue → branch → PR → merge. Never commit directly to main again. After a month, look at your issue history — it will be a readable record of everything you built and why.
2. Ask someone (a friend, a parent, anyone) to read one of your PR descriptions and tell you if they can understand what changed and why. If they cannot, rewrite it.
