# Version Control

The are many version control systems, but this document is only about using `git`. This content is mostly similar to [this great guide](https://github.com/git-guides/), but with my take on when to do various actions.

## The basics

Git is powerful version control software that lets you save your work in a variety of powerful ways. It was originally built for a large distributed team working on the Linux operating system kernel, but it works great for individuals as well. Because it was designed for managing code, it does not work as well for managing the state of images or complex document formats like PDFs or Word documents, but it certainly still could be used for them.

### The types of saves

Git has three main states a change can be in: uncommitted, staged, and committed.

1. An uncommitted change is something that you are currently editing.
    - To see what uncomitted changes you have made to existing files, use `git diff`.
2. A staged change is the result of using `git add <file>`, and represents work that you think is done, but are still reviewing.
    - To see what staged changes you have, use `git diff --cached`.
3. And a committed change is work that you have staged and then comitted with `git commit`.
    - To see recent commits, use `git log`. On GitHub, you can see a file's commits in its History page and click on a commit to see what changes it made.

![git-staging-area](https://git-scm.com/images/about/index1@2x.png)

_[image from git-scm.org](https://git-scm.com/about/staging-area)_

At any point you can see the state of everything with `git status`.

```terminal
❯ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes to be committed:
  (use "git restore --staged <file>..." to unstage)
        modified:   README.md

Untracked files:
  (use "git add <file>..." to include in what will be committed)
        version_control.md
        writing_code.md
```

## Commit what works

Commits are best used to save work that you know "works," which could mean many different things depends on what you're working on.

To commit something, you must first stage it with `git add` and then commit it with `git commit`. Commiting requires a description of what the commit does. These are often brief descriptions of what changed, although some people are into writing long commit messages.

```terminal
❯ git add version_control.md
❯ git commit -m "This change adds instructions for how to commit"
```

In any type of writing you can undo, but with git you can also revert back to the latest commit. This is powerful if you only commit code that works; no matter how bad things get, you can revert your work back to a known good state with `git restore`.

```terminal
❯ git status
On branch main
Your branch is up to date with 'origin/main'.

Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)
  (use "git restore <file>..." to discard changes in working directory)
        modified:   README.md

no changes added to commit (use "git add" and/or "git commit -a")

❯ git restore README.md
Updated 1 path from the index

❯ git status
On branch main
Your branch is up to date with 'origin/main'.

nothing to commit, working tree clean
```
