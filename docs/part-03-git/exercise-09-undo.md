---
title: "3.9 Undoing Mistakes"
parent: Git and History
nav_order: 9
---

# Exercise 3.9 — Undoing Mistakes

## The Story

Here are four real situations engineers find themselves in. Read each one and notice what you would feel in that moment.

---

**Situation A:** You are editing `library.py`. You change the search function trying to make it faster. It breaks completely. You have not committed anything. You just want your working file back.

*What would you do without Git?* Ctrl+Z until you hope you got back far enough, or hunt for a backup copy.

---

**Situation B:** You are cleaning up before a commit. You run `git add .` to stage all your changes. Then you realise you accidentally staged a half-finished, broken feature that was not ready. You do not want to throw away the work — you just do not want it in this commit.

*What would you do without Git?* You would have to commit the broken feature, or throw away all your staged changes and start over.

---

**Situation C:** You commit a change to the library. Three seconds later, you read the commit message and see a typo. Or you look at the diff and realise you accidentally left in a debug `print("HERE")` statement. The commit is done, but you haven't pushed it yet.

*What would you do without Git?* Nothing — it is committed. You would either live with it or make another commit to fix it, polluting the history.

---

**Situation D:** You accidentally delete `library.py`. Or the whole `src/` folder. You stare at the empty directory. The file manager's Recycle Bin is empty. There is no Ctrl+Z in the terminal.

*What would you do without Git?* Panic. Hope for a backup. Probably start over.

---

**Situation E:** You pushed a commit that introduced a serious bug. Other people have already pulled it. You cannot just delete the commit — that would break their copies. But the bug needs to be undone.

*What would you do without Git?* Manually reverse every change and commit a "fix." But which changes? In which files?

---

In every one of these situations, Git has an answer. The important thing is not memorising commands — it is understanding *what kind of situation you are in* and *why Git can help*.

## What to Do

### Scenario A — You broke a file and want it back

**Live through it:** Edit `library.py` and deliberately break the search function — change it so it crashes. Do NOT commit. Now try to "undo" it using the file manager or Ctrl+Z. Notice that this is unreliable. You do not know how many times to undo, and the editor may not remember that far back.

**The insight:** Git has a clean copy of this file — it is the last committed version. You never committed the broken change. So Git's version is still the working one.

**The question to ask yourself:** What is Git holding that I don't have?

**The question answered:** After running the restoration, look at the file. It is exactly the last committed version. Git did not guess or approximate — it went back to a known good state.

**Practice:** Break three different things in your library, one at a time. Before restoring each, write down: what did I break, and what is Git holding that I want back? Restore each one and confirm it worked.

---

### Scenario B — You staged the wrong thing

**Live through it:** Make two changes to your library at the same time:
1. Fix a real bug (something small and complete)
2. Start a half-finished feature (something that makes the program error)

Now run `git add .` — both changes are staged. Run `git status` and look at what you are about to commit. You are about to commit a broken, half-finished feature alongside a real fix.

**The insight:** Staging is not permanent. Git has a concept of "I am planning to commit this" (staged) which is separate from "I have committed this." You can change your plan before committing.

**The question to ask yourself:** Can I undo a staged change without losing the edit itself?

**Practice:** Unstage *only* the half-finished feature, leaving the bug fix staged. Verify with `git status` that the bug fix is still staged and the half-finished feature is back to being just an edit. Then commit only the bug fix. Commit the feature separately later.

---

### Scenario C — You committed something small and wrong

**Live through it:** Make a commit. Then immediately look at `git log` and notice the message says "Add search feture" (typo). Or run `git show HEAD` and see you left a `print("debugging")` inside.

**The insight:** A commit is not carved in stone until you push it. Before sharing it with anyone, you can change it. This is different from a pushed commit — the key question is: *has anyone else received this commit?*

**The question to ask yourself:** Have I pushed this yet? If no — I can still change it. If yes — I must handle it differently to avoid breaking others.

**Practice:** Make a commit with a deliberate typo in the message. Notice the discomfort. Then repair it so that `git log` shows the corrected message. Make another commit where you accidentally include a debug print statement. Fix it so the commit looks like the print was never there.

---

### Scenario D — You deleted a file (or a whole folder)

**Live through it:** This is the most frightening scenario. Do it deliberately so you know you can recover.

1. Delete `README.md` from the terminal (or file manager). It is gone from disk. Check that it is really gone — it is not in the Recycle Bin or Trash.

Now stop. Before doing anything else, ask: *does Git still know about this file?*

Run `git status`. Git will show `README.md` as deleted — but Git still has a copy. The last committed version of that file exists in the Git history. Git only "forgets" a file when you commit the deletion and tell it to.

**The insight:** Deleting a file from disk is not the same as deleting it from Git history. Until you commit the deletion, Git is still holding the last committed version. Even after committing the deletion, the file still exists in every earlier commit — you can reach back and get it.

2. Recover the deleted `README.md`. Confirm it is back.

3. Now do the harder version: delete `README.md`, then *stage the deletion* (tell Git you intend to commit the removal). Check `git status` — Git now knows you plan to remove it. Can you still recover it? Try.

4. Now the hardest version: delete a file, stage it, commit it. The file is gone from the current version of the project. Run `git log` — do any previous commits still show this file? Can you get it back from those?

**The question to ask yourself at each stage:** How far has the deletion "traveled into Git"? Has it just happened on disk? Been staged? Been committed? The answer tells you how to recover.

5. Finally — delete the entire `src/` folder if you have one. Or create a temporary folder with a couple of files, commit it, then delete the whole folder. Recover it.

**Practice:** After recovering each deletion, write one sentence: *why was Git able to give me back something that was deleted from my disk?*

---

### Scenario E — You pushed a commit that needs to be undone

**Live through it:** Push a commit that "accidentally removes the search feature" (you can simulate this by commenting out the search function and committing). Now imagine a colleague has already pulled this commit. They have it on their machine.

**The insight:** Git's history is shared once it is pushed. If you delete or change a past commit now, your colleague's copy and your copy will have different histories — Git will refuse to work with them together, or produce chaos. The only safe way forward is to *add* a new commit that undoes the old one. The bad commit stays in history, but the new commit cancels it out.

**The question to ask yourself:** Is the damage in the past (something I can cancel by adding to the future), or do I need to pretend it never happened? If other people have the commit — you can only add, not erase.

**Practice:** Push the "broken" commit. Then add a new commit that restores what was removed. The history will show: "removed search feature" then "restore search feature." That is honest and safe. The alternative — pretending the first commit never existed — is only possible before pushing, and causes problems for teams.

---

## The Mental Model

Before reaching for any Git command, ask three questions:

1. **What did I lose or break?** (A file? An edit? A commit message?)
2. **How far has it gone?** (Just on disk? Staged? Committed? Pushed?)
3. **Has anyone else received it?** (Only matters for committed/pushed situations)

The answers to these questions tell you what kind of recovery is possible. The specific commands follow from the situation — they are not the thing to memorise.

## Before You Start — Think About This

1. You accidentally delete a file that was never committed to Git. Can Git help you? Why or why not? What does this tell you about the relationship between committing and safety?
2. In Scenario E, why does it matter whether someone else has pulled the bad commit? What would happen to their copy of the repository if you simply deleted the commit from your history?
3. Some engineers commit after every tiny change, even when it feels unnecessary. After this exercise, do you understand why? What are they protecting themselves from?

## When You're Stuck

- `git status` is always the first thing to run. It tells you exactly what state each file is in right now — whether changes are unstaged, staged, or committed.
- If you are not sure whether a file is recoverable, run `git log --all -- filename`. If the file appears in the output, Git has it somewhere and you can get it back.
- `git reflog` shows every action Git has taken in your repository — even resets and checkouts. If you feel you have lost something irretrievably, check here first.

## Once It Works — Go Further

1. Before this exercise, were you afraid to delete things, afraid to make "bad" commits, afraid to try changes? After the exercise, has that fear changed? Write one sentence about what changed in how you think about working with Git.
2. A professional engineer once said: "I commit every 20 minutes, not because the work is done, but because I want a recovery point every 20 minutes." Does that make sense to you now?
