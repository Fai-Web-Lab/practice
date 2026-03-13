# Learning Git and GitHub!

## Table of Contents

- [Software Interfaces](#1-software-interfaces)
- [Git Internals: The Hidden Database](#2-git-internals-the-hidden-database)
- [File States & Lifecycle](#3-file-states--lifecycle)
- [Advanced Command Reference](#4-advanced-command-reference)
- [Branching, Merging & History Rewriting](#5-branching-merging--history-rewriting)
- [Stashing & Work in Progress (WIP)](#6-stashing--wip)
- [GitHub Collaboration](#7-github-collaboration)

---

## 1. Software Interfaces

Understanding how we interact with systems.

- `CMD` (Command Line): The command line interface allows users to interact with the system by entering commands.  

Workflow:
`Input → Processing → Output`
The system receives an input, processes it, calls the necessary function, and returns an output.

---

- `GUI` (Graphical User Interface): The graphical interface focuses on simplicity and usability.  

Users interact with the system through:  
- buttons
- menus
- visual components

---

- `API` (Application Programming Interface): An API allows interaction with systems using structured requests.  

Example:
```
www.Tuwaiq.com/Sum?a=5&b=2
```
The server processes the request and returns the result.

- Core Idea

Regardless of the interface type:


Input → Processing → Output


The goal is always the same:  
**Send an input and receive a meaningful output.**

---

# 2. Git Internals: The Hidden Database

Git is not just a version control tool. Internally, Git behaves like a **content-addressable filesystem**. Every object stored in Git is identified using a **SHA-1 hash**.

---

- SHA-1 Hash

A **40-character hexadecimal string** uniquely identifies each Git object.

Example:


e83c5163316f89bfbde7d9ab23ca2e25604af290


---

## Storage Optimization

Git organizes objects efficiently.

- The first **2 characters** of the hash create a directory
- The remaining **38 characters** form the file name

Example:


.git/objects/e8/3c5163316f89bfbde7d9ab23ca2e25604af290


This prevents having too many files in a single directory.

---

## Compression

Git compresses stored objects to:

- save disk space
- maintain data integrity

---

## The Four Fundamental Git Objects

Git stores data using four main object types.

### Blob

A **Blob (Binary Large Object)** stores the **actual file content**.

It does not include:

- file name
- file path

---

### Tree

A **Tree object** represents a directory.

It stores references (hashes) to:

- blobs (files)
- other trees (subdirectories)

---

### Commit

A **Commit** represents a snapshot of the project at a specific moment.

It contains metadata such as:

- Author name
- Author email
- Date
- Commit message
- Pointer to the tree object

---

### Tag

A **Tag** is a permanent reference to a specific commit ID.

Tags do not move and are typically used for:

- releases
- version labels

Example:


v1.0
v2.0


---

# 3. File States & Lifecycle

Files move through a defined lifecycle in Git.


Working Directory → Staging Area → Repository


---

## Untracked

Files that Git has never seen before.

They are not included in commits.

You can exclude files using:


.gitignore


---

## Unmodified

Files that have been committed and have **no changes**.

---

## Modified (Dirty)

Files that have been changed in the **working directory** but are **not yet staged**.

---

## Staged (Index)

Files that have been moved to the **staging area** and are ready for commit.

Example:

```bash
git add file.txt
4. Advanced Command Reference
Configuration & Setup

Initialize a repository:

git init

Configure Git identity:

git config --global user.name "Your Name"
git config --global user.email "you@example.com"

Customize command prompt:

export PS1="dev: "
Committing & Inspecting

Commit staged files:

git commit -m "message"

Shortcut to stage and commit modified files:

git commit -a -m "msg"

Modify the last commit:

git commit --amend

View commit history in short format:

git log --oneline

View differences between files:

git diff

Check the type of a Git object:

git cat-file -t <hash>
5. Branching, Merging & History Rewriting
Branching

Branches allow parallel development.

Create and switch to a new branch:

git checkout -b <branch-name>
Merging
Fast-Forward Merge

Occurs when the main branch has not diverged.

Git simply moves the branch pointer forward.

3-Way Merge

Occurs when branches have different histories.

Git creates a new merge commit combining both branches.

Reset (History Rewriting)
Soft Reset
git reset --soft HEAD~1

Removes the commit but keeps changes staged.

Mixed Reset
git reset --mixed HEAD~1

Removes the commit and unstages the changes, but keeps them in the working directory.

Hard Reset
git reset --hard HEAD~1

Deletes the commit and all associated changes permanently.

Cherry-Pick

Apply a specific commit to the current branch.

git cherry-pick <commit-id>
Rebase

Rebase changes the base of your branch to another branch head.

git rebase main

This helps create a clean and linear history.

6. Stashing & Work in Progress (WIP)

When work is not ready to commit, Git allows you to temporarily store it.

Save Work
git stash

Moves current changes to a temporary stack.

Restore Work

Restore and remove the latest stash:

git stash pop

Restore but keep a copy in the stash:

git stash apply
7. GitHub Collaboration

GitHub enables collaborative development on top of Git.

Fork

A fork creates a copy of a repository under another GitHub account.

Clone

Creates a local copy of a repository.

git clone <repository-url>
Pull Request (PR)

A Pull Request is used to propose changes to the original repository.

Typical workflow:

Fork the repository

Clone it locally

Create a branch

Make changes

Push the branch

Open a Pull Request

Remote Connections

Git repositories communicate using remote connections.

Typical structure:

Local Repository (Downstream)
        ↓
Remote Repository (Upstream)
