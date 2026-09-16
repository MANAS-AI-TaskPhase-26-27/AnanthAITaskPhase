# Basic Git and GitHub Commands

A quick reference for common Git and GitHub commands, including basic branching and merging.

---

## 1. What is Git?

**Git** is a distributed version control system used to track changes in files and collaborate on projects.

**GitHub** is a cloud platform where Git repositories can be stored, shared, and collaborated on.

---

# 2. Git Configuration

### Set your username

```bash
git config --global user.name "Your Name"
```

Sets the name that Git associates with your commits.

### Set your email

```bash
git config --global user.email "you@example.com"
```

Sets the email associated with your commits.

### Check configuration

```bash
git config --list
```

Displays the current Git configuration.

---

# 3. Creating a Repository

### Initialize a Git repository

```bash
git init
```

Creates a new Git repository in the current folder.

### Clone an existing repository

```bash
git clone <repository-url>
```

Downloads a remote repository to your computer.

Example:

```bash
git clone https://github.com/username/project.git
```

### Check repository status

```bash
git status
```

Shows modified files, staged files, untracked files, and the current branch.

---

# 4. Basic Git Workflow

The basic Git workflow is:

```text
Working Directory
       |
       v
     git add
       |
       v
 Staging Area
       |
       v
   git commit
       |
       v
 Local Repository
       |
       v
    git push
       |
       v
 Remote Repository (GitHub)
```

---

# 5. Tracking Changes

### Check changes

```bash
git status
```

Shows the current state of your working directory.

### View changes that are not staged

```bash
git diff
```

Shows changes made to files that have not been staged.

### Add one file to staging

```bash
git add filename
```

Adds a specific file to the staging area.

### Add all changed files

```bash
git add .
```

Stages all changes in the current directory.

### Commit changes

```bash
git commit -m "Your commit message"
```

Creates a commit containing the staged changes.

Example:

```bash
git commit -m "Added login page"
```

### View commit history

```bash
git log
```

Shows the commit history.

### Compact commit history

```bash
git log --oneline
```

Shows commits in a shorter format.

---

# 6. GitHub Remote Commands

A **remote** is a connection between your local Git repository and a repository hosted somewhere such as GitHub.

### Add a GitHub remote

```bash
git remote add origin <repository-url>
```

Connects your local repository to a GitHub repository.

Example:

```bash
git remote add origin https://github.com/username/project.git
```

### View remotes

```bash
git remote -v
```

Shows the URLs of configured remote repositories.

### Rename a branch

```bash
git branch -M main
```

Renames the current branch to `main`.

### Push a branch to GitHub

```bash
git push -u origin main
```

Uploads the local `main` branch to GitHub.

The `-u` option sets `origin/main` as the upstream branch, so later you can usually use:

```bash
git push
```

### Push changes

```bash
git push
```

Uploads committed changes to the remote repository.

### Download remote changes

```bash
git pull
```

Fetches changes from the remote repository and integrates them into the current branch.

### Fetch remote changes without merging

```bash
git fetch
```

Downloads information about changes from the remote repository without changing your current working branch.

---

# 7. Basic Branching

A **branch** is a separate line of development. Branches allow you to work on features or fixes without directly changing the main branch.

Typical structure:

```text
main
 |
 |------ feature-login
 |
 |------ feature-dashboard
 |
 |------ bug-fix
```

## List branches

```bash
git branch
```

Shows local branches.

### List local and remote branches

```bash
git branch -a
```

Shows both local and remote branches.

### Create a branch

```bash
git branch <branch-name>
```

Creates a new branch but does not switch to it.

Example:

```bash
git branch feature-login
```

### Switch to a branch

```bash
git switch <branch-name>
```

Moves to an existing branch.

Example:

```bash
git switch feature-login
```

### Create and switch to a new branch

```bash
git switch -c <branch-name>
```

Creates a new branch and immediately switches to it.

Example:

```bash
git switch -c feature-login
```

Older Git syntax:

```bash
git checkout -b feature-login
```

---

# 8. Working on a Branch

Example workflow:

```bash
git switch -c feature-login
```

Make your changes, then:

```bash
git status
```

Stage the changes:

```bash
git add .
```

Commit them:

```bash
git commit -m "Added login feature"
```

Push the branch to GitHub:

```bash
git push -u origin feature-login
```

---

# 9. Merging Branches

**Merging** combines the changes from one branch into another branch.

Suppose you have:

```text
main
 |
 A---B
             C---D  feature-login
```

You want to merge `feature-login` into `main`.

### Step 1: Switch to the branch receiving the changes

```bash
git switch main
```

### Step 2: Merge the feature branch

```bash
git merge feature-login
```

The changes from `feature-login` are now incorporated into `main`.

After a successful merge:

```text
A---B-------E  main
     \     /
       C---D
       feature-login
```

### Push the merged changes

```bash
git push
```

---

# 10. Merge Conflicts

A **merge conflict** happens when Git cannot automatically decide which changes to keep.

For example, two branches may modify the same part of a file.

Git may mark the file like this:

```text
<<<<<<< HEAD
Code from the current branch
=======
Code from the branch being merged
>>>>>>> feature-login
```

### Basic conflict-resolution process

1. Open the conflicted file.
2. Decide which changes should remain.
3. Remove the conflict markers:
   - `<<<<<<<`
   - `=======`
   - `>>>>>>>`
4. Save the file.
5. Stage the resolved file:

```bash
git add filename
```

6. Complete the merge:

```bash
git commit
```

Then push the result:

```bash
git push
```

### Abort a merge

If you want to cancel an ongoing merge:

```bash
git merge --abort
```

This attempts to return the repository to its state before the merge started.

---

# 11. Deleting Branches

### Delete a local branch

```bash
git branch -d <branch-name>
```

Deletes a local branch after it has been merged.

Example:

```bash
git branch -d feature-login
```

### Force-delete a local branch

```bash
git branch -D <branch-name>
```

Force-deletes the branch even if Git considers it unmerged.

### Delete a remote branch

```bash
git push origin --delete <branch-name>
```

Deletes the branch from the remote repository.

Example:

```bash
git push origin --delete feature-login
```

---

# 12. Useful Git Commands

### Show the current branch

```bash
git branch --show-current
```

Displays the branch you are currently on.

### Show commit details

```bash
git show
```

Displays information about the most recent commit.

### Undo unstaged changes in a file

```bash
git restore filename
```

Restores the file to its last committed/staged state.

> Be careful: this can discard changes that have not been committed.

### Unstage a file

```bash
git restore --staged filename
```

Removes a file from the staging area while keeping its changes in the working directory.

### Create a tag

```bash
git tag <tag-name>
```

Creates a tag pointing to the current commit.

### Show tags

```bash
git tag
```

Lists available tags.

---

# 13. Common Git + GitHub Workflow

For a new project:

```bash
mkdir my-project
cd my-project
git init
```

Create or add your files, then:

```bash
git add .
git commit -m "Initial commit"
```

Connect to GitHub:

```bash
git remote add origin <repository-url>
git branch -M main
git push -u origin main
```

For later changes:

```bash
git add .
git commit -m "Updated project"
git push
```

---

# 14. Feature Branch Workflow

A common workflow for adding a new feature is:

```bash
# Start from main
git switch main

# Get the latest version
git pull

# Create a feature branch
git switch -c feature-name

# Make changes

# Stage changes
git add .

# Commit changes
git commit -m "Added new feature"

# Push feature branch to GitHub
git push -u origin feature-name
```

After the feature is complete, it can be merged into `main`:

```bash
git switch main
git pull
git merge feature-name
git push
```

Then the feature branch can be deleted if it is no longer needed:

```bash
git branch -d feature-name
git push origin --delete feature-name
```

---

# 15. Git Command Cheat Sheet

| Command | Use |
|---|---|
| `git init` | Create a Git repository |
| `git clone <url>` | Copy a remote repository |
| `git status` | Check repository status |
| `git add <file>` | Stage a file |
| `git add .` | Stage all changes |
| `git commit -m "message"` | Save staged changes as a commit |
| `git log` | View commit history |
| `git diff` | View unstaged changes |
| `git branch` | List branches |
| `git branch <name>` | Create a branch |
| `git switch <name>` | Switch branches |
| `git switch -c <name>` | Create and switch to a branch |
| `git merge <branch>` | Merge a branch |
| `git merge --abort` | Cancel an ongoing merge |
| `git branch -d <name>` | Delete a local branch |
| `git remote -v` | View remote repositories |
| `git remote add origin <url>` | Add a remote |
| `git fetch` | Download remote changes without merging |
| `git pull` | Download and integrate remote changes |
| `git push` | Upload commits to GitHub |
| `git push -u origin <branch>` | Push a new branch and set upstream |
| `git restore <file>` | Discard unstaged file changes |
| `git restore --staged <file>` | Unstage a file |

---

# 16. The Most Important Commands to Remember

If you are just starting with Git, focus on these first:

```bash
git init
git clone <url>
git status
git add .
git commit -m "message"
git push
git pull
git branch
git switch -c <branch>
git switch <branch>
git merge <branch>
```

The basic cycle is:

```text
Make changes
     ↓
git status
     ↓
git add .
     ↓
git commit -m "message"
     ↓
git push
```

For branches:

```text
main
 ↓
git switch -c feature
 ↓
Make changes
 ↓
git add .
 ↓
git commit
 ↓
git push
 ↓
git switch main
 ↓
git merge feature
 ↓
git push
```
