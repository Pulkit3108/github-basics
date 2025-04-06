# Learning Git Basics

## Git Workflow and Commands

This README provides an overview of Git along with common commands for merging, rebasing, and squashing commits. It also explains advanced commands to safely manage your commit history, such as force pushing and handling rebase conflicts.

## What is Git?

Git is a distributed version control system that tracks changes in source code during software development. It enables multiple developers to collaborate, maintain a history of changes, and easily revert to previous states when necessary.

## Basic Git Commands

### Git Fetch

**Purpose:**  
Download objects and refs from a remote repository without integrating them into your working directory.

**Command:**
```bash
git fetch [remote-name]
```

**Example:**
```bash
# Fetch all branches from origin
git fetch origin

# Fetch from all remotes
git fetch --all
```

**Note:** Fetching is a safe way to see changes without merging them into your local branches.

### Git Pull

**Purpose:**  
Fetch and integrate changes from a remote repository into the current branch (essentially a `git fetch` followed by a `git merge`).

**Command:**
```bash
git pull [remote-name] [branch-name]
```

**Example:**
```bash
# Pull changes from the origin remote's main branch
git pull origin main
```

**Pull All Branches:**
```bash
# Update all local branches that track remote branches
git pull --all
```

### Git Cherry-Pick

**Purpose:**  
Apply a specific commit from one branch to another.

**Command:**
```bash
git cherry-pick <commit-hash>
```

**Example:**
```bash
# Apply commit abc123 to the current branch
git cherry-pick abc123
```

**Multiple Commits:**
```bash
# Cherry-pick a range of commits
git cherry-pick abc123..def456
```

**Note:** Cherry-picking is useful when you want to apply specific changes without merging entire branches.

## Git Merge

**Purpose:**  
Combine changes from one branch into another while preserving the history of both branches.

**Command:**
```bash
git merge <branch-name>
```

**Example:**
```bash
# Switch to the target branch (e.g., master)
git checkout master

# Merge changes from the feature branch into master
git merge feature-branch
```

**Note:** Merging creates a merge commit if there are divergent changes, maintaining a non-linear history.

## Git Rebase

**Purpose:**  
Reapply commits from one branch onto another to create a linear project history.

**Command:**
```bash
git rebase <base-branch>
```

**Example:**
```bash
# Switch to your feature branch
git checkout feature-branch

# Rebase your feature branch onto master
git rebase master
```

### Handling Conflicts During Rebase

**Continue Rebase:**  
Once you've resolved any conflicts, continue the rebase process with:
```bash
git rebase --continue
```

**Abort Rebase:**  
If you want to cancel the rebase process and return to your original state:
```bash
git rebase --abort
```

**Note:** Rebasing rewrites commit history. You can use it on local or private branches to avoid conflicts with collaborators.

## Git Squash

**Purpose:**  
Combine multiple commits into a single commit. This is useful for cleaning up your commit history before merging into the main branch.

**Command:**
```bash
git rebase -i HEAD~<number-of-commits>
```

**Example:**
```bash
# Squash the last 3 commits into one
git rebase -i HEAD~3
```

**Steps:**
1. An editor opens with a list of commits.
2. Change `pick` to `squash` (or `s`) for the commits you want to combine.
3. Save and close the editor to complete the squash process.

## Advanced Git Commands

### Git Push with Force

**Command:**
```bash
git push --force-with-lease
```

**Explanation:**  
This command force pushes your local branch to the remote repository but does so safely by ensuring that the remote branch is in the expected state. It prevents accidentally overwriting changes made by others.

---

This document is a quick reference guide for essential Git commands and workflows. Experiment in a safe environment to become more comfortable with these commands and understand their effects on your project's history.
