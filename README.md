## Git Commands: Zero to Hero
A practical guide, organized by workflow and objective.

### **I. The Absolute Fundamentals (Zero)**
*These are the commands you'll use 90% of the time.*

| Command | Description | Example |
| :--- | :--- | :--- |
| `git init` | Initialize a new Git repo in the current folder. | `git init` |
| `git clone <url>` | Download a remote repository to your machine. | `git clone https://github.com/user/repo.git` |
| `git status` | **Your best friend.** Shows the state of your working directory and staging area. | `git status` |
| `git add <file>` | Stage a specific file for the next commit. | `git add index.html` |
| `git add .` | Stage **all** new and modified files for the next commit. | `git add .` |
| `git commit -m "msg"` | Take a snapshot of the staged changes with a descriptive message. | `git commit -m "Add login button"` |
| `git push origin <branch>` | Upload your local commits to a remote repository (like GitHub). | `git push origin main` |
| `git pull origin <branch>` | Download changes from the remote and merge them into your current branch. | `git pull origin main` |

---

### **II. Branching & Context Switching (Novice)**
*Working on multiple features without messing up the main code.*

| Command | Description | Example |
| :--- | :--- | :--- |
| `git branch` | List all local branches. The `*` shows your current branch. | `git branch` |
| `git branch <name>` | Create a new branch based on your current commit. | `git branch new-feature` |
| `git checkout <branch>` | Switch to an existing branch. | `git checkout new-feature` |
| `git checkout -b <name>` | **Create a new branch and switch to it immediately.** (Very common) | `git checkout -b fix-bug` |
| `git switch <branch>` | Newer, clearer way to switch branches (Git 2.23+). | `git switch main` |
| `git switch -c <name>` | Newer way to create and switch to a branch. | `git switch -c new-feature` |
| `git merge <branch>` | Combine the specified branch's history into your current branch. | `git switch main` <br> `git merge new-feature` |
| `git branch -d <branch>` | Delete a branch that has been merged (safe delete). | `git branch -d old-feature` |
| `git branch -D <branch>` | **Force delete a branch,** even if it hasn't been merged. (Be careful!) | `git branch -D abandoned-experiment` |

---

### **III. Undoing Mistakes & Rewriting History (Apprentice)**
*The "oh crap" moments. Use these carefully.*

| Command | Description | When to Use |
| :--- | :--- | :--- |
| `git restore <file>` | Discard changes in your working directory for a specific file. | "I haven't `add`ed this file yet and I want to start over." |
| `git restore --staged <file>` | Unstage a file **without** losing the changes in your working directory. | "I `add`ed the wrong file by accident." |
| `git commit --amend` | **Edit the most recent commit.** Change the message or add forgotten files. | "I just committed but forgot a file!" or "My commit message has a typo." |
| `git reset --soft HEAD~1` | Undo the last commit but **keep all your changes as staged**. | "I want to combine my last two commits." |
| `git reset --hard HEAD~1` | **Completely obliterate** the last commit and all its changes. **Warning: Unrecoverable.** | "That last commit was a huge mistake, I want to pretend it never happened." |
| `git revert <commit-hash>` | Create a *new commit* that undoes the changes of a previous commit. **Safe for public history.** | "I need to undo a commit I already pushed to others." |

---

### **IV. Advanced History Manipulation (Hero)**
*For a clean, professional commit history.*

| Command | Description | Use Case |
| :--- | :--- | :--- |
| `git rebase <branch>` | Replay your current branch's commits on top of the latest version of `<branch>`. | "I want a clean, linear history for my feature branch before merging." |
| `git rebase -i HEAD~3` | **Interactive Rebase.** Opens an editor to squash, edit, reorder, or drop commits. | "I have 5 messy 'WIP' commits I want to combine into one clean commit." |
| `git cherry-pick <commit>` | Apply the changes from a specific commit to your current branch. | "I need just that one bugfix from another branch, not the whole thing." |
| `git stash` | Temporarily shelves (stashes) all your uncommitted changes. | "My boss needs a fix NOW, but I'm in the middle of something." |
| `git stash pop` | Re-apply your most recently stashed changes and remove them from the stash. | "Okay, boss's fix is done, back to my feature." |

---

### **V. Inspecting & Comparing (Detective)**
*Figuring out what happened and when.*

| Command | Description |
| :--- | :--- |
| `git log` | Show the commit history. |
| `git log --oneline --graph --all` | Fancy, compact history view with branch topology. **Memorize this.** |
| `git diff` | Show unstaged changes since the last commit. |
| `git diff --staged` | Show staged changes (what you've `add`ed). |
| `git blame <file>` | Show who last modified each line of a file and in which commit. |

---

### **VI. Synchronizing with a Remote (Collaborator)**
*Working with others on GitHub/GitLab.*

| Command | Description |
| :--- | :--- |
| `git fetch origin` | Download all changes from the remote **without** merging them. "See what others have done." |
| `git pull --rebase origin main` | **Best practice pull.** Fetches remote changes and rebases your commits on top of them. Cleaner than a merge. |
| `git push origin --delete <branch>` | Delete a branch on the remote (e.g., after merging a Pull Request). |
| `git remote -v` | Show the URLs of your connected remote repositories. |

---

## How to Organize Your `git-scenarios-guide` Project

Based on the commands above, you can structure your repo with clear scenarios. Here’s a proposed folder structure:

```
git-scenarios-guide/
├── 01-basics/
│   ├── init-and-commit.md
│   ├── cloning-a-repo.md
│   └── checking-status.md
├── 02-branching/
│   ├── creating-branches.md
│   ├── merging.md
│   └── deleting-branches.md
├── 03-undoing-things/    # This is a goldmine for your guide!
│   ├── discard-changes.md          # `git restore`
│   ├── unstage-a-file.md           # `git restore --staged`
│   ├── amend-last-commit.md        # `git commit --amend`
│   ├── soft-reset.md               # `git reset --soft`
│   ├── hard-reset-warning.md       # `git reset --hard` (with big warnings)
│   └── revert-a-commit.md          # `git revert`
├── 04-advanced/
│   ├── interactive-rebase.md
│   ├── cherry-picking.md
│   └── stashing-changes.md
└── 05-collaboration/
    ├── fetching-vs-pulling.md
    ├── rebase-pull.md
    └── deleting-remote-branches.md
```

---

## Deleting a Git Repository

To delete an initialized Git directory, you need to remove the `.git` folder. Here's how to do it:

## Step 1: Check if it's a Git repository
```bash
ls -la
```
Look for the `.git` directory in the output. If you see it, you're in a Git repository.

## Step 2: Remove the Git repository

### Option A: Delete just the .git folder (keeps your files)
```bash
rm -rf .git
```

### Option B: Delete the entire directory (including all files)
```bash
# First, navigate out of the directory if you're inside it
cd ..

# Then delete the entire directory
rm -rf your-directory-name/
```

## Step 3: Verify it's no longer a Git repo
```bash
ls -la
```
The `.git` folder should be gone. You can also check with:
```bash
git status
```
This should show: `fatal: not a git repository (or any of the parent directories): .git`

## Example workflow:
```bash
# 1. Check what's in the directory
$ ls -la
total 12
drwxr-xr-x  3 user user 4096 Dec 10 14:30 .
drwxr-xr-x 10 user user 4096 Dec 10 14:30 ..
drwxr-xr-x  7 user user 4096 Dec 10 14:30 .git  # This is what we want to remove
-rw-r--r--  1 user user   23 Dec 10 14:30 README.md

# 2. Remove the .git folder
$ rm -rf .git

# 3. Verify it's gone
$ ls -la
total 8
drwxr-xr-x  2 user user 4096 Dec 10 14:31 .
drwxr-xr-x 10 user user 4096 Dec 10 14:30 ..
-rw-r--r--  1 user user   23 Dec 10 14:30 README.md

# 4. Confirm it's no longer a Git repo
$ git status
fatal: not a git repository (or any of the parent directories): .git
```

## Important Notes:
- `rm -rf` is **permanent** - deleted files cannot be easily recovered
- If you want to keep your files but remove Git tracking, use `rm -rf .git`
- If you want to delete everything including your files, use `rm -rf your-directory-name/`
- Be very careful with `rm -rf` - double-check you're in the right directory!

## Alternative: Use a file manager
You can also delete the `.git` folder using your system's file manager (Finder on Mac, File Explorer on Windows) by showing hidden files and deleting the `.git` folder.
