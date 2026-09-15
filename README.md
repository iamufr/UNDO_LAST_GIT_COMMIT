# HOW TO SAFELY UNDO THE LAST PUSHED GIT COMMIT

This guide explains a standard Git workflow for undoing a mistake that has already been pushed to a remote repository (like GitHub). 

## When to Use This Workflow
Use these commands when you accidentally commit and push broken code, sensitive data, or incorrect files, and you need to reverse those changes. 

This specific method is the **safest way** to undo a mistake because it does not delete history. Instead of erasing your mistake (which can cause errors for teammates sharing your branch), it creates a *brand new commit* that does the exact opposite of your last commit.

## The Commands Explained

### 1. Check your status

```bash
git status
```

**What it does:** Checks the current state of your repository.
**Why we use it:** To make sure you have no uncommitted changes and that you are on the correct branch (usually `main`) before starting the revert process.

### 2. Undo the mistake

```bash
git revert HEAD
```

**What it does:** Undoes the changes made in the very last commit (`HEAD`).
**Why we use it:** This is the core command. It looks at everything you changed in your last commit and creates a new commit that perfectly reverses it (e.g., if you added a line, it removes it; if you deleted a file, it brings it back).
*Note: This command will open your terminal's text editor (like Vim) asking you to save the new commit message. On Mac, you type `:wq` and press Enter to save and exit.*

### 3. Verify it worked

```bash
git log -1
```

**What it does:** Shows the history of your most recent commit. (`-1` means just the last one).
**Why we use it:** To verify that the revert worked. You should see a brand new commit at the top of your history that starts with "Revert...".

### 4. Send the fix to GitHub

```bash
git push origin main
```

**What it does:** Uploads your new revert commit to GitHub.
**Why we use it:** Your local computer has fixed the mistake, but GitHub doesn't know that yet. Pushing updates the remote repository so the mistake is officially undone for everyone.

---