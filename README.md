# Git & GitHub 

Git is one of the most important tools in DevOps because DevOps engineers constantly work with source code, configuration files, infrastructure code, CI/CD pipelines, and deployment files.

Think of Git as a version-control system that tracks every important change you make to your project.

### 📄 Complete Notes

👉 **[Open Git & GitHub Complete Guide](./git-and-github.pdf)**

---
---

## 1. Git vs GitHub

This is the first thing you should understand clearly.

### Git

**Git = Version Control System**

Git is software installed on your computer that tracks changes in your files.

**Example:**

You have `index.html`. Initially: `Hello World`. You change it to: `Hello DevOps`.

Git can remember:
```
Version 1 → Hello World
Version 2 → Hello DevOps
```

So if you make a mistake, you can go back to an older version.

### GitHub

**GitHub = Cloud platform for hosting Git repositories.**

Git works locally on your computer. GitHub allows you to store your Git repository online and collaborate with others.

```
Git
 ↓
Your computer
 ↓
Tracks changes
```

```
GitHub
 ↓
Internet / Cloud
 ↓
Stores your Git repository
 ↓
Collaboration
```

**Simple analogy**

- Think of Git as Microsoft Word's version history.
- GitHub is like Google Drive, where you store and share the project.

> Git ≠ GitHub. Git is the tool. GitHub is a platform that works with Git repositories.

---

## 2. Repository

A **repository (repo)** is a project that Git is tracking.

**Example:**
```
my-website/
├── index.html
├── style.css
├── script.js
└── README.md
```

When Git tracks this project, it becomes a Git repository. A Git repository contains a hidden directory: `.git/`

The `.git` directory contains Git's internal information about your project history.

> ⚠️ Don't manually modify `.git` unless you know exactly what you're doing.

---

## 3. Working Directory

The **working directory** is the actual files you're currently working on.

**Example:**
```
my-project/
├── index.html
├── style.css
└── README.md
```

You open `index.html` and modify it. That modification first exists in your working directory.

---

## 4. Staging Area

The **staging area** is where you tell Git: *"I want these changes to be included in my next commit."*

**Example:**

You modify `index.html`, `style.css`, `README.md`, but you only want to commit `index.html` and `style.css`.

You stage them:
```bash
git add index.html
git add style.css
```

```
Working Directory
       ↓
   git add
       ↓
Staging Area
```

---

## 5. Commit

A **commit** is a saved checkpoint in Git history.

**Example:**
```bash
git commit -m "Add homepage"
```

This creates a permanent-ish point in your local Git history.

> Think of a commit as: 📸 A snapshot of your project at a particular point in time.

Good commit messages:
- `Add login page`
- `Fix database connection`
- `Update Docker configuration`

---

## 6. The Most Important Git Workflow

**Memorize this:**

```
Working Directory
       ↓
    git add
       ↓
Staging Area
       ↓
  git commit
       ↓
Local Repository
       ↓
   git push
       ↓
GitHub Repository
```

This is extremely important for DevOps.

---

## 7. Branch

A **branch** allows you to work on changes separately from the main code.

Imagine:
```
main
 │
 ├── commit 1
 ├── commit 2
 └── commit 3
```

You create `feature-login`:
```
main
 │
 ├── commit 1
 ├── commit 2
 └── commit 3
          \
           feature-login
             │
             ├── commit 4
             └── commit 5
```

You can develop the login feature without directly changing `main`.

**Common branches:** `main`, `develop`, `feature-login`, `feature-payment`, `bugfix-login`

---

## 8. Merge

After finishing your feature, you may want to combine it with `main`. That's called a **merge**.

**Example:**
```
main
 │
 ├── A
 ├── B
 │
 └─────────────┐
               │
feature-login  │
 │             │
 ├── C         │
 └── D         │
               ↓
             merge
               ↓
             main
```

**Command:**
```bash
git switch main
git merge feature-login
```

Now the changes from `feature-login` are incorporated into `main`.

---

## 9. Remote Repository

A **remote repository** is a Git repository located somewhere else, usually on a service such as GitHub.

**Example:**
```
Your Mac
   │
   │ Git
   ↓
Local Repository
   │
   │ git push
   ↓
GitHub
   │
   ↓
Remote Repository
```

Usually the remote is named `origin`. Check it with:
```bash
git remote -v
```

Example output:
```
origin  git@github.com:username/project.git
```

---

## 10. HEAD

**HEAD** means: *The commit/branch you are currently pointing to.*

For example:
```
A ← B ← C
        ↑
       HEAD
```

If you're on `main` at commit C:
```
HEAD → main → C
```

When you create a new commit:
```
A ← B ← C ← D
            ↑
           HEAD
```

Understanding HEAD becomes particularly important when learning: `git reset`, `git checkout`, `git switch`, `git revert`

---

## 11. .gitignore

`.gitignore` tells Git: *"Don't track these files."*

**Example:**
```
node_modules/
.env
*.log
.DS_Store
```

**Why?** You usually don't want to upload:
- passwords
- API keys
- secret files
- temporary files
- large generated files
- dependencies

For example, `.env` might contain:
```
DB_PASSWORD=secret123
AWS_ACCESS_KEY=xxxxx
```

> You should never commit secrets to GitHub.

---

## Git Commands

Now let's understand the commands one by one.

### 12. `git init`

Creates a new Git repository.

```bash
mkdir my-project
cd my-project
git init
```

Git creates:
```
my-project/
└── .git/
```

Now Git starts tracking the project. Check with `git status`.

### 13. `git clone`

Used to copy an existing remote repository to your computer.

```bash
git clone https://github.com/username/project.git
```

Git downloads the repository:
```
project/
├── files
├── README.md
└── .git/
```

You normally use clone when you already have a project on GitHub.

### 14. `git status`

Shows the current state of your repository.

```bash
git status
```

Example output:
```
modified: index.html
untracked: app.js
```

It tells you: modified files, untracked files, staged files, current branch.

> You should use this command very frequently.

### 15. `git add`

Moves changes into the staging area.

```bash
git add index.html              # one file
git add index.html style.css    # multiple files
git add .                       # everything
```

```
Working Directory
       ↓
    git add .
       ↓
Staging Area
```

### 16. `git commit`

Creates a commit from staged changes.

```bash
git commit -m "Add homepage"
```

The `-m` means message.

- ✅ Good: `git commit -m "Add EC2 deployment script"`
- ❌ Bad: `git commit -m "changes"`

Your commit messages should describe what changed.

### 17. `git push`

Uploads your local commits to the remote repository.

```bash
git push
```

Typical flow:
```
Local commit
     ↓
git push
     ↓
GitHub
```

Example:
```bash
git add .
git commit -m "Add networking notes"
git push
```

Now GitHub has your changes.

### 18. `git pull`

Downloads changes from the remote repository and integrates them into your current branch.

```bash
git pull
```

```
GitHub
   ↓
git pull
   ↓
Your computer
```

Example: Your friend changes `README.md` and pushes it to GitHub. You run `git pull` — now you receive the changes.

### 19. `git fetch`

Downloads information about changes from the remote repository **without** merging those changes into your current branch.

```bash
git fetch
```

```
GitHub
   ↓
git fetch
   ↓
Download information
   ↓
You inspect changes
```

Then you can decide what to do.

**pull vs fetch** (very important):

```
git fetch
    ↓
Download remote changes
    ↓
Does NOT automatically merge into your current branch
```

```
git pull
    ↓
Fetch + Integrate changes
```

Simplified: `git pull ≈ git fetch + integration`

### 20. `git branch`

View branches:
```bash
git branch
```

Example:
```
* main
  feature-login
  development
```

The `*` means your current branch.

Create a branch:
```bash
git branch feature-login
```

### 21. `git checkout`

Historically used to switch branches:
```bash
git checkout feature-login
```

Older Git workflows commonly use it. You can also create and switch:
```bash
git checkout -b feature-login
```

This means: create branch + switch to branch.

### 22. `git switch`

Modern Git provides `git switch` specifically for branch switching.

```bash
git switch feature-login        # switch
git switch -c feature-login     # create + switch
```

> Recommended: learn the modern syntax `git switch` for branch operations.

### 23. `git merge`

Combines changes from one branch into another.

```bash
git switch main
git merge feature-login
```

Meaning: merge `feature-login` into `main`.

> ⚠️ Direction matters. If you are on `main` and run `git merge feature-login`, you're bringing `feature-login` into `main`.

### 24. `git log`

Shows commit history.

```bash
git log
```

Example:
```
commit abc123
Author: Adi
Message: Add login page

commit def456
Author: Adi
Message: Add homepage
```

A cleaner view:
```bash
git log --oneline
```

Example:
```
abc123 Add login page
def456 Add homepage
789xyz Initial commit
```

Very useful for understanding project history.

### 25. `git diff`

Shows differences between versions.

Suppose you change `Hello World` to `Hello DevOps`. Run:
```bash
git diff
```

Git shows what changed — think of it as: *"What did I modify?"*

### 26. `git stash`

Temporarily stores your uncommitted changes.

Imagine you're working on `feature-login` with unfinished work. Suddenly your manager says: *"There is a bug in production. Fix it immediately."*

You don't want to commit unfinished work. Run:
```bash
git stash
```

Your working directory becomes clean. Now switch branches:
```bash
git switch main
```

Fix the bug. Later return:
```bash
git switch feature-login
git stash pop
```

Flow:
```
Uncommitted work
       ↓
   git stash
       ↓
Temporarily stored
       ↓
Do other work
       ↓
   git stash pop
       ↓
Changes restored
```

### 27. `git reset`

`git reset` moves HEAD and can change what is staged or what is in your working directory, depending on the mode.

> This is a command you should understand carefully because some forms can discard work.

**Common example:** unstage a file
```bash
git reset HEAD file.txt
```
This removes the file from the staging area while keeping your file changes.

**Three common modes:**
```bash
git reset --soft
git reset --mixed
git reset --hard
```

Conceptually:

| Mode | HEAD | Staged Changes | Working Changes |
|---|---|---|---|
| `--soft` | Moves | Remain staged | Kept |
| `--mixed` | Moves | Become unstaged | Kept |
| `--hard` | Moves | Discarded | Can be discarded |

> ⚠️ Be very careful with `git reset --hard` because it can permanently discard uncommitted work.

### 28. `git revert`

`git revert` creates a **new commit** that reverses an earlier commit.

Suppose commit C introduced a bug:
```
A → B → C
```

Instead of deleting history:
```bash
git revert C
```

Git creates:
```
A → B → C → D
```
where D reverses the changes made by C.

This is generally safer for shared branches such as `main`.

**reset vs revert** (important for DevOps interviews):

**Reset** — moves branch history backward:
```
A → B → C
        ↓
      reset
        ↓
A → B
```

**Revert** — creates a new commit that undoes previous changes:
```
A → B → C
        ↓
      revert
        ↓
A → B → C → D
```

> For shared/public history, revert is usually preferred because it doesn't rewrite the existing commit history.

---

## GitHub

Now let's move from Git to GitHub.

### 29. Create a GitHub Repository

On GitHub, you can create a repository such as `devops-learning`:

```
devops-learning/
│
├── Linux/
├── Networking/
├── AWS/
├── Git/
├── Docker/
└── README.md
```

This is actually a good way to demonstrate your DevOps learning to recruiters.

### 30. SSH Authentication

SSH allows your computer to authenticate with GitHub using an SSH key. Instead of repeatedly entering credentials:

```
Your Mac
   │
   │ SSH key
   ↓
GitHub
```

Typical process:
```bash
ssh-keygen -t ed25519 -C "your-email@example.com"
```

This creates an SSH key pair: a **private key** and a **public key**.

- The private key stays on your computer.
- The public key is added to GitHub.

> ⚠️ Never share your private SSH key.

Your repository URL can then look like:
```
git@github.com:username/project.git
```

Test the connection:
```bash
ssh -T git@github.com
```

### 31. Personal Access Token (PAT)

A **Personal Access Token** is a credential used for GitHub authentication in situations where a token is required instead of a password.

```
Username + Password
        ↓
        ❌
```

GitHub commonly uses `Username + Personal Access Token`, or preferably an **SSH key**, for Git operations.

> ⚠️ Never publish your PAT in GitHub, README, Git repository, or screenshots. Treat it like a password.

### 32. Pull Request (PR)

A **Pull Request** is a request to merge changes from one branch into another.

```
main
  ↑
  │
Pull Request
  │
feature-login
```

**Developer workflow:**
```
Create feature branch
        ↓
Write code
        ↓
git add
        ↓
git commit
        ↓
git push
        ↓
Create Pull Request
```

Then another developer can: review code, comment, request changes, approve.

After approval:
```
feature-login
      ↓
     PR
      ↓
    main
```

### 33. Branch Protection

**Branch protection rules** help prevent dangerous changes to important branches.

For example, you can protect `main` and require:
```
Pull Request + Code review + Status checks
```
before merging.

This is very common in professional DevOps environments.

**Typical workflow:**
```
Developer
   ↓
Feature branch
   ↓
Pull Request
   ↓
Code Review
   ↓
CI tests
   ↓
Approval
   ↓
main
```

### 34. README

`README.md` explains what your project is about.

**Example:**
```markdown
# AWS Learning

## Topics
- EC2
- S3
- IAM
- VPC
- EBS
- Auto Scaling

## Projects
- EC2 Web Server
- S3 Static Website
- VPC Architecture
```

GitHub automatically displays the README on your repository's main page.

> For your DevOps learning, good README files are useful because they show recruiters what you learned + what you actually practiced.

### 35. GitHub Actions Basics

This is where Git and DevOps start connecting directly.

**GitHub Actions = CI/CD automation platform built into GitHub.**

Example: you push code, GitHub detects the push, then GitHub Actions can automatically:
```
Code pushed
    ↓
GitHub Actions
    ↓
Run tests
    ↓
Build application
    ↓
Deploy application
```

Example workflow:
```
Developer
   ↓
git push
   ↓
GitHub
   ↓
GitHub Actions
   ↓
Test
   ↓
Build
   ↓
Deploy
```

This is the foundation of CI/CD.

A GitHub Actions workflow is usually stored here:
```
.github/
└── workflows/
    └── ci.yml
```

A workflow can say:
```
When code is pushed:
    ↓
Checkout code
    ↓
Install dependencies
    ↓
Run tests
    ↓
Build application
```

Later in your DevOps learning, you'll connect this with:
```
Git → GitHub → GitHub Actions → Docker → AWS → Deployment
```

---

## 🔥 Complete Git Workflow Example

Let's imagine you're building a website.

**Step 1 — Create project**
```bash
mkdir my-website
cd my-website
```

**Step 2 — Initialize Git**
```bash
git init
```

**Step 3 — Create files**
```
index.html
style.css
```

**Step 4 — Check status**
```bash
git status
```
Git might show:
```
Untracked files:
    index.html
    style.css
```

**Step 5 — Stage**
```bash
git add .
```

**Step 6 — Commit**
```bash
git commit -m "Initial website"
```

Now:
```
Working Directory
       ↓
    git add
       ↓
Staging Area
       ↓
  git commit
       ↓
Local Repository
```

**Step 7 — Create GitHub repository**

Create `my-website` on GitHub.

**Step 8 — Connect local repo to GitHub**

For SSH:
```bash
git remote add origin git@github.com:USERNAME/my-website.git
```

**Step 9 — Push**
```bash
git push -u origin main
```

Now:
```
Your Mac
   ↓
Local Git Repository
   ↓
git push
   ↓
GitHub
```

---

## 🔥 Feature Development Example

Now you need to add a login page.

**Create a branch:**
```bash
git switch -c feature-login
```

**Work on:** `login.html`

**Check:**
```bash
git status
```

**Stage:**
```bash
git add login.html
```

**Commit:**
```bash
git commit -m "Add login page"
```

**Push the branch:**
```bash
git push -u origin feature-login
```

Then on GitHub:
```
feature-login
      ↓
Pull Request
      ↓
Code Review
      ↓
Approval
      ↓
Merge
      ↓
main
```

That's a real-world development workflow.

---

## 🧠 The Git Architecture You Should Memorize

This is probably the most important diagram for today's lesson:

```
                 GITHUB
              Remote Repository
                    ↑
                    │
                 git push
                    │
            LOCAL REPOSITORY
               Git History
                    ↑
                    │
                git commit
                    │
              STAGING AREA
                    ↑
                    │
                 git add
                    │
             WORKING DIRECTORY
              Your actual files
```

And for downloading:
```
GitHub
   │
   ├── git clone → First time download
   │
   ├── git fetch → Get remote information/changes without integrating
   │
   └── git pull  → Fetch + integrate changes
```

---

## 🧠 Commands Cheat Sheet

| Command | Purpose |
|---|---|
| `git init` | Create Git repository |
| `git clone` | Copy remote repository |
| `git status` | Check repository state |
| `git add` | Stage changes |
| `git commit` | Create checkpoint |
| `git push` | Upload commits |
| `git pull` | Fetch + integrate remote changes |
| `git fetch` | Download remote information/changes without integrating |
| `git branch` | View/create branches |
| `git checkout` | Older command for switching branches |
| `git switch` | Switch branches |
| `git merge` | Combine branches |
| `git log` | View commit history |
| `git diff` | View changes |
| `git stash` | Temporarily store uncommitted changes |
| `git reset` | Move/reset HEAD and potentially staging/worktree |
| `git revert` | Create a commit that reverses another commit |

