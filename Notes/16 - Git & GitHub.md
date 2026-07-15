# Git & GitHub — Interview Preparation Guide

## Table of Contents

1. [1. What is Git?](#1-what-is-git)
2. [2. What is GitHub?](#2-what-is-github)
3. [3. Git vs GitHub](#3-git-vs-github)
4. [4. What is a repository?](#4-what-is-a-repository)
5. [5. What is a commit?](#5-what-is-a-commit)
6. [6. What is a branch?](#6-what-is-a-branch)
7. [7. What is the default branch?](#7-what-is-the-default-branch)
8. [8. What is `git init`?](#8-what-is-git-init)
9. [9. What is `git clone`?](#9-what-is-git-clone)
10. [10. What is `git status`?](#10-what-is-git-status)
11. [11. What is `git add`?](#11-what-is-git-add)
12. [12. What is the staging area?](#12-what-is-the-staging-area)
13. [13. What is `git commit`?](#13-what-is-git-commit)
14. [14. What is `git log`?](#14-what-is-git-log)
15. [15. What is `git diff`?](#15-what-is-git-diff)
16. [16. What is `git push`?](#16-what-is-git-push)
17. [17. What is `git pull`?](#17-what-is-git-pull)
18. [18. What is `git fetch`?](#18-what-is-git-fetch)
19. [19. `git fetch` vs `git pull`](#19-git-fetch-vs-git-pull)
20. [20. What is `git merge`?](#20-what-is-git-merge)
21. [21. What is a merge conflict?](#21-what-is-a-merge-conflict)
22. [22. How do you resolve a merge conflict?](#22-how-do-you-resolve-a-merge-conflict)
23. [23. What is `git rebase`?](#23-what-is-git-rebase)
24. [24. `merge` vs `rebase`](#24-merge-vs-rebase)
25. [25. What is `git checkout`?](#25-what-is-git-checkout)
26. [26. What is `git switch`?](#26-what-is-git-switch)
27. [27. What is `git restore`?](#27-what-is-git-restore)
28. [28. What is `git reset`?](#28-what-is-git-reset)
29. [29. What is `git revert`?](#29-what-is-git-revert)
30. [30. `git reset` vs `git revert`](#30-git-reset-vs-git-revert)
31. [31. What is `git stash`?](#31-what-is-git-stash)
32. [32. What is `git cherry-pick`?](#32-what-is-git-cherrypick)
33. [33. What is `HEAD` in Git?](#33-what-is-head-in-git)
34. [34. What is detached HEAD?](#34-what-is-detached-head)
35. [35. What is `.gitignore`?](#35-what-is-gitignore)
36. [36. Why use `.gitignore`?](#36-why-use-gitignore)
37. [37. What is a remote repository?](#37-what-is-a-remote-repository)
38. [38. What is `origin` in Git?](#38-what-is-origin-in-git)
39. [39. What is a pull request?](#39-what-is-a-pull-request)
40. [40. Why are pull requests important?](#40-why-are-pull-requests-important)
41. [41. What is a fork in GitHub?](#41-what-is-a-fork-in-github)
42. [42. What is a code review?](#42-what-is-a-code-review)
43. [43. What is branch protection in GitHub?](#43-what-is-branch-protection-in-github)
44. [44. What is GitHub Actions?](#44-what-is-github-actions)
45. [45. What is a workflow in GitHub Actions?](#45-what-is-a-workflow-in-github-actions)
46. [46. What is a runner in GitHub Actions?](#46-what-is-a-runner-in-github-actions)
47. [47. What is a Git tag?](#47-what-is-a-git-tag)
48. [48. What is branching strategy?](#48-what-is-branching-strategy)
49. [49. What is the difference between local and remote branch?](#49-what-is-the-difference-between-local-and-remote-branch)
50. [50. Important Git best practices](#50-important-git-best-practices)

## 1. What is Git?
Git is a **distributed version control system** used to track changes in code, manage collaboration, and maintain version history.

---

## 2. What is GitHub?
GitHub is a **cloud platform for hosting Git repositories** and supporting collaboration through pull requests, code reviews, issues, and workflows.

---

## 3. Git vs GitHub
- **Git** is the version control tool
- **GitHub** is a platform built around Git for hosting and collaboration

---

## 4. What is a repository?
A **repository** is a project folder tracked by Git. It contains code, commit history, branches, and configuration.

---

## 5. What is a commit?
A **commit** is a snapshot of changes saved in the repository history.

---

## 6. What is a branch?
A **branch** is an independent line of development used to work on features or fixes without affecting the main code immediately.

---

## 7. What is the default branch?
The default branch is usually **main** or **master**, depending on repository setup.

---

## 8. What is `git init`?
`git init` creates a new local Git repository.

---

## 9. What is `git clone`?
`git clone` copies an existing remote repository to your local machine.

---

## 10. What is `git status`?
`git status` shows the current state of the working directory and staging area.

---

## 11. What is `git add`?
`git add` moves changes from the working directory to the **staging area**.

---

## 12. What is the staging area?
The **staging area** is an intermediate space where changes are prepared before commit.

---

## 13. What is `git commit`?
`git commit` saves staged changes into the repository history.

---

## 14. What is `git log`?
`git log` shows the commit history of the repository.

---

## 15. What is `git diff`?
`git diff` shows differences between file versions, branches, commits, or staged and unstaged changes.

---

## 16. What is `git push`?
`git push` uploads local commits to a remote repository.

---

## 17. What is `git pull`?
`git pull` fetches changes from the remote repository and merges them into the current branch.

---

## 18. What is `git fetch`?
`git fetch` downloads remote changes but does not merge them automatically.

---

## 19. `git fetch` vs `git pull`
- **fetch** only downloads changes
- **pull** downloads and merges changes

---

## 20. What is `git merge`?
`git merge` combines changes from one branch into another.

---

## 21. What is a merge conflict?
A **merge conflict** happens when Git cannot automatically combine changes because the same part of code was modified differently.

---

## 22. How do you resolve a merge conflict?
I resolve it by:
- opening the conflicted files
- choosing the correct final code
- removing conflict markers
- staging the fixed files
- committing the merge

---

## 23. What is `git rebase`?
`git rebase` moves or reapplies commits from one branch onto another base commit, creating a cleaner linear history.

---

## 24. `merge` vs `rebase`
- **merge** preserves branch history
- **rebase** creates a cleaner linear history
In teams, rebase is useful locally, but shared branch history should be handled carefully.

---

## 25. What is `git checkout`?
Traditionally, `git checkout` is used to switch branches or restore files. In newer Git, `git switch` and `git restore` are clearer alternatives.

---

## 26. What is `git switch`?
`git switch` is used to switch branches.

---

## 27. What is `git restore`?
`git restore` is used to discard file changes or restore file content.

---

## 28. What is `git reset`?
`git reset` moves the current branch pointer and can unstage or remove commits depending on the mode.

---

## 29. What is `git revert`?
`git revert` creates a new commit that undoes a previous commit safely without rewriting history.

---

## 30. `git reset` vs `git revert`
- **reset** rewrites history
- **revert** preserves history by adding an undo commit
For shared branches, `revert` is usually safer.

---

## 31. What is `git stash`?
`git stash` temporarily saves uncommitted changes so you can work on something else and reapply them later.

---

## 32. What is `git cherry-pick`?
`git cherry-pick` applies a specific commit from one branch onto another branch.

---

## 33. What is `HEAD` in Git?
`HEAD` is a pointer to the current commit or current checked-out branch.

---

## 34. What is detached HEAD?
A **detached HEAD** state happens when you check out a specific commit instead of a branch. You can inspect code there, but commits made in that state can be lost unless attached to a branch.

---

## 35. What is `.gitignore`?
`.gitignore` is a file used to tell Git which files or folders should not be tracked.

---

## 36. Why use `.gitignore`?
It is used to ignore:
- `node_modules`
- build files
- environment files
- logs
- OS/editor-generated files

---

## 37. What is a remote repository?
A **remote repository** is a repository hosted on a server or platform like GitHub.

---

## 38. What is `origin` in Git?
`origin` is the default name commonly given to the main remote repository.

---

## 39. What is a pull request?
A **pull request** is a request to merge code changes from one branch into another, usually after review.

---

## 40. Why are pull requests important?
Pull requests help with:
- code review
- discussion
- quality control
- approval workflow
- safer collaboration

---

## 41. What is a fork in GitHub?
A **fork** is a copy of someone else’s repository under your own account, commonly used in open-source contribution.

---

## 42. What is a code review?
A **code review** is the process of examining code changes before merging them to ensure quality, readability, and correctness.

---

## 43. What is branch protection in GitHub?
Branch protection is a GitHub feature that prevents direct unsafe changes to important branches by requiring checks, approvals, or restrictions.

---

## 44. What is GitHub Actions?
GitHub Actions is GitHub’s built-in automation and CI/CD system used for testing, building, linting, and deployments.

---

## 45. What is a workflow in GitHub Actions?
A **workflow** is an automated process defined in YAML that runs on certain events like push or pull request.

---

## 46. What is a runner in GitHub Actions?
A **runner** is the machine that executes the workflow jobs.

---

## 47. What is a Git tag?
A **tag** is a named reference to a specific commit, often used for releases like `v1.0.0`.

---

## 48. What is branching strategy?
A **branching strategy** is the team’s way of organizing development branches, releases, and merges.

### Common strategies:
- feature branching
- Git Flow
- trunk-based development

---

## 49. What is the difference between local and remote branch?
- **local branch** exists on your machine
- **remote branch** exists on the remote repository like GitHub

---

## 50. Important Git best practices
- commit small, meaningful changes
- write clear commit messages
- pull frequently
- avoid pushing broken code
- use branches for features/fixes
- do not commit secrets
- review before merging

---

# Most Important Commands for Interview Revision

```bash
git init
git clone <repo-url>
git status
git add .
git commit -m "message"
git log
git diff
git branch
git switch <branch>
git checkout <branch>
git pull
git fetch
git push
git merge <branch>
git rebase <branch>
git stash
git stash pop
git reset
git revert <commit>
git cherry-pick <commit>