
# Git
<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

---

## 1. What is a Version Control System (VCS)?

* A **Version Control System** is software that records changes to files over time so you can recall specific versions later.
* Without VCS, you’d manually create copies like `project_v1`, `project_final`, `project_final_final`, which quickly becomes chaotic.


## 2. Difference Between DVCS and CVCS

### Centralized VCS (CVCS)

* One **central server** stores the repository.
* Developers **check out** files, edit them, then check back in.
* Requires **constant network connection**.
* If server goes down, nobody can collaborate.
* Examples: **Subversion (SVN), CVS, Perforce**.

### Distributed VCS (DVCS)

* Every developer has the **full repository (with history)** on their machine.
* Developers can commit offline, then sync later.
* Faster operations (commits, diffs, logs are local).
* Safer – if central server is lost, any developer can restore it.
* Examples: **Git, Mercurial, Bazaar**.

| Feature             | CVCS (Centralized)            | DVCS (Distributed)            |
| ------------------- | ----------------------------- | ----------------------------- |
| Repository location | Single central server         | Every developer has full copy |
| Offline support     | No                            | Yes                           |
| Speed               | Slower (network dependency)   | Faster (local ops)            |
| Fault tolerance     | Server crash = data loss risk | Safer (multiple backups)      |
| Examples            | SVN, CVS                      | Git, Mercurial                |

---

## 3. What is Git?

* **Git** is the world’s most popular **Distributed Version Control System (DVCS)**.
* Created in **2005 by Linus Torvalds** for Linux kernel development.
* It became popular because of its:

  * **Speed** (optimized for large codebases).
  * **Data Integrity** (uses SHA-1 hashes).
  * **Distributed nature** (no single point of failure).
  * **Efficient branching and merging**.


## 4. Git Installation & Setup

### Installation

* **Ubuntu/Debian**

  ```bash
  sudo apt update
  sudo apt install git -y
  ```
* **CentOS/Fedora**

  ```bash
  sudo dnf install git -y
  ```
* **MacOS**

  ```bash
  brew install git
  ```
* **Windows**

  * Install **Git for Windows** from [git-scm.com](https://git-scm.com).

### Initial Setup (First-time config)

```bash
git config --global user.name "Bubu"
git config --global user.email "bubu@example.com"
```

* Check config:

  ```bash
  git config --list
  ```

* Change default branch from `master` to `main`:

  ```bash
  git config --global init.defaultBranch main
  ```

---

## 5. Git Architecture

<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/gitarchitecture.png" alt="Banner" />


Git operates in **four main areas**:

1. **Working Directory (or Working Tree):**

   * Your project files.
   * When you edit a file, it becomes **modified**.

2. **Staging Area (Index):**

   * A snapshot of changes you want to commit.
   * Files are moved here using `git add`.

3. **Local Repository (.git folder):**

   * Permanent store of all commits and history.
   * Created when you run `git init`.

4. **Remote Repository:**

   * Hosted on platforms like **GitHub, GitLab, Bitbucket**.
   * Shared repo for collaboration.

🔑 **Data Flow:**

```
Working Directory → Staging Area → Local Repo → Remote Repo
```

---

## 6. Basic Git Commands



* Initialize repository:

  ```bash
  git init
  ```

* Check file states:

  ```bash
  git status
  ```
* Stage files:
  to stage a single file called file.txt
  ```bash
  git add file.txt
  ```
  
  to stage all files in a specific directory
  ```
  git add .   # all changes
  ```
  
* Commit changes:
  
  to commit the changes to git local repository
  
  ```bash
  git commit -m "your commit message"
  ```
  
* Skip staging (direct commit):

  ```bash
  git commit -am "Quick commit"
  ```

### History & Info

* Show commits:

  ```bash
  git log
  git log --oneline --graph --decorate --all
  ```
* Show differences:
  
These two Git commands are used to show differences (a "diff") between different stages of your local repository, but they compare different things:

| Command | Compares | What it shows |
|---|---|---|
| `git diff` | **Working Directory** vs. **Staging Area** (or Index) | The changes you have made to files since the last time you ran `git add` on them. These are your **unstaged changes**. |
| `git diff --staged` | **Staging Area** (or Index) vs. **Last Commit** (`HEAD`) | The changes that have been added to the staging area (using `git add`) and are ready to be included in the next commit. These are your **staged changes**. |

### brief:

* `git diff` : We use git diff to see what has changed in your project — line by line — before you commit or between different commits, branches, or files..
* `git diff --staged` tells you: **"What's in the staging area that is ready to be committed and is different from the last shipped box?"** (Staged changes).


### 🧱 **Git Areas and diff commands**

```
             ┌────────────────────────────┐
             │        Repository          │
             │     (Last commit - HEAD)   │
             └────────────┬───────────────┘
                          ▲
                          │  git diff --staged
                          │  (Staging area ↔ Repo)
                          │
             ┌────────────┴───────────────┐
             │        Staging Area        │
             │    (Files you git add-ed)  │
             └────────────┬───────────────┘
                          ▲
                          │  git diff
                          │  (Working dir ↔ Staging)
                          │
             ┌────────────┴───────────────┐
             │     Working Directory      │
             │  (Your actual files now)   │
             └────────────────────────────┘
```

---

### 💡 Summary

| Command                             | Compares                               | Shows                                   |
| ----------------------------------- | -------------------------------------- | --------------------------------------- |
| `git diff`                          | Working Directory ↔ Staging Area       | What you **changed but not yet staged** |
| `git diff --staged` (or `--cached`) | Staging Area ↔ Last Commit (HEAD)      | What you **staged for commit**          |




## 7. Branching in Git

A **branch** in Git is just a pointer to a commit.
Think of branches like **different storylines in a book**. The main story (`main` branch) is always stable, but you can create alternate storylines (branches) to try out new ideas without messing up the main plot.

---

## 1. List Branches

```bash
git branch
```

* Shows all branches in your repository.
* The branch with a `*` (star) is your **current branch**.

Example output:

```
* main
  feature1
  bugfix
```

👉 Here, you are on `main`. There are two other branches available.

---

## 2. Create a New Branch

```bash
git branch feature1
```

* Creates a branch called `feature1`.
* **Important:** This only *creates* the branch, it does **not switch** to it.

Analogy: You opened a new blank notebook to write a story, but you haven’t started writing in it yet.

---

## 3. Switch to a Branch

```bash
git checkout feature1
```

* Switches you from your current branch to `feature1`.
* Now, any commits you make will go into the `feature1` branch.

Modern alternative (recommended):

```bash
git switch feature1
```

Analogy: You now opened the new notebook and started writing in it.

---

## 4. Create & Switch in One Step

```bash
git checkout -b bugfix
```

* Creates a new branch called `bugfix` **and** switches to it immediately.
* Saves time (instead of running `git branch` + `git checkout`).

Modern alternative:

```bash
git switch -c bugfix
```

👉 Useful when starting work on a new feature or bugfix quickly.


---

## 6. Delete a Branch

```bash
git branch -d feature1
```

* Deletes the branch named `feature1`.
* Safe to delete only after merging into `main`.
* Git prevents deletion if the branch has unmerged changes.

To **force delete** (not recommended unless sure):

```bash
git branch -D feature1
```

Analogy: Once a side storyline is merged into the main story, you throw away the draft copy.


# 🌳 Visualizing Branches

Use:

```bash
git log --oneline --graph --decorate --all
```

Example output:

```
*   3f2d1c4 (HEAD -> main) Merge branch 'feature-login'
|\
| * a2b3d4e (feature-login) Added login feature
* | 1a2b3c4 Initial project setup
```


## **Git Merge**

The primary purpose of `git merge` is to integrate changes from one branch into another. When you execute a merge, Git takes two commit pointers (usually the tips of two branches) and attempts to find a common ancestor commit, then combines the changes from both histories.

### **1. The Mechanics: How to Merge**

The general workflow for merging is:

1.  **Switch to the Target Branch:** You must be on the branch you want to merge *into*. This branch will receive the new changes.
    ```bash
    git checkout target-branch
    ```
2.  **Execute the Merge:** Run the merge command, specifying the source branch whose changes you want to incorporate.
    ```bash
    git merge source-branch
    ```
    *The `target-branch` is updated, but the `source-branch` remains unaffected.*

### **2. Types of Merges**

Git automatically determines the most appropriate merge strategy based on the history of the branches. The two main types are:

#### **A. Fast-Forward Merge**

<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/fastforward.png" alt="Banner" />


A fast-forward merge occurs when there is a **linear path** from the tip of the current branch (`target-branch`) to the tip of the branch being merged (`source-branch`).

  * **When it happens:** If the `target-branch` has not diverged (i.e., no new commits have been added since the `source-branch` was created), Git can simply move the pointer of the `target-branch` forward to the latest commit of the `source-branch`.
  * **Result:** **No new merge commit is created.** The history remains linear and clean, as if the commits were made directly on the `target-branch`.
  * **Controlling it:** To *force* Git to create a merge commit even if a fast-forward is possible (for record-keeping), use the `--no-ff` option:
    ```bash
    git merge --no-ff source-branch
    ```

#### **B. Three-Way (Recursive) Merge**
<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/recursive.png" alt="Banner" />


A three-way merge occurs when the branches have **diverged**—commits have been added to *both* the `target-branch` and the `source-branch` since they split from their common ancestor.

  * **How it works:** Git uses three commits to determine the changes to combine:
    1.  The tip of the `target-branch`.
    2.  The tip of the `source-branch`.
    3.  The **common ancestor** (or *merge base*).
        Git calculates the difference between the ancestor and both branch tips, then applies both sets of changes to the ancestor state.
  * **Result:** A **new merge commit** is created. This commit is special because it has *two* parent commits, effectively tying the two divergent histories back together. This preserves the history of both branches and shows exactly where the integration occurred. This is the default behavior when branches have diverged.

### **3. Merge Conflicts**

The biggest challenge with merging is the potential for **merge conflicts**.

  * **When they occur:** A conflict happens when Git cannot automatically decide how to combine changes because the **same lines** in the **same file** have been modified differently in both branches since the common ancestor.
  * **Process:**
    1.  Git pauses the merge process and marks the files with conflicts.
    2.  You will see **conflict markers** in the conflicting files:
        ```
        <<<<<<< HEAD
        This is the change on the target-branch (HEAD).
        =======
        This is the change on the source-branch being merged.
        >>>>>>> source-branch
        ```
    3.  **Manual Resolution:** You must manually edit the file, remove the conflict markers, and decide which version (or a combination of both) of the code to keep.
    4.  **Complete the Merge:**
          * Stage the resolved file(s): `git add <conflicted-file>`
          * Commit the merge: `git commit` (Git will usually provide a default merge message).
  * **Aborting:** If you decide you don't want to complete the merge, you can abort the process and return to the state before the merge attempt:
    ```bash
    git merge --abort
    ```

### **4. Merge Strategies (Advanced)**

Git has several merge strategies, though the default, **`recursive`**, is the most common and robust for merging two branches.

  * **`recursive` (Default for 2 branches):** The standard three-way merge. It is generally safe and can handle complex cases, including detecting and handling renames.
  * **`octopus` (Default for $>2$ branches):** Used for merging more than two heads (branches). It will refuse to perform a merge that requires manual conflict resolution.
  * **`ours`:** The result of the merge is always the contents of the current branch (`HEAD`), effectively ignoring all changes from the other branch(es). This is typically used to record that a feature branch has been incorporated, even if its changes are to be discarded.


### **Summary**

`git merge` is the standard tool for integrating parallel work in Git. It is crucial for combining feature or bug-fix branches into stable branches like `main`. Understanding the difference between a **Fast-Forward** and a **Three-Way Merge** is key to managing your repository's history effectively, and knowing how to resolve **Merge Conflicts** is essential for collaborative development.


## 8. Merge vs Rebase

### Git Merge

* Combines two branches.
* Creates a **merge commit**.
* Keeps full history (non-linear).

```bash
git checkout main
git merge feature
```

### Git Rebase

* Moves commits from one branch on top of another.
* Creates a **linear history** (no merge commits).
* Rewrites commit history → dangerous if branch is public.

```bash
git checkout feature
git rebase main
```

| Merge                    | Rebase                   |
| ------------------------ | ------------------------ |
| Preserves branch history | Rewrites history         |
| Easier for teamwork      | Cleaner, linear history  |
| Always safe              | Risky on shared branches |

👉 Rule: **Use merge for teamwork, rebase for cleaning your local commits.**

---

# 🧰 **Git Stash**

## 📘 **Definition**

`git stash` is a command used to **temporarily save (or "stash") changes** in your working directory that are **not yet ready to be committed**, allowing you to work on something else (like switching branches) without losing your uncommitted work.

Think of it like putting your ongoing work in a **“temporary locker”** — you can retrieve it later and continue from where you left off.

---

## 🧩 **When to Use Git Stash**

You typically use `git stash` when:

* You have **uncommitted changes** but need to **switch branches**.
* You want to **pull updates** from remote but your working directory isn’t clean.
* You want to **test something quickly** without committing your current modifications.
* You need to **temporarily save work** for later.

---

## ⚙️ **How Git Stash Works**

When you run `git stash`, Git:

1. Takes the changes in:

   * The **working directory** (unstaged changes)
   * The **staging area** (staged changes)
2. Saves them in a **new stash object** inside `.git/refs/stash`.
3. Reverts your working directory to the **last committed state** (clean working tree).

---

## 💻 **Common Git Stash Commands**

### 1. 🏁 **Save Changes to a Stash**

```bash
git stash
```

* Saves both **staged** and **unstaged** changes.
* Does **not** stash untracked files (like new files not added with `git add`).

You can give a description to your stash:

```bash
git stash save "WIP: fixing login bug"
```

or

```bash
git stash push -m "WIP: fixing login bug"
```

---

### 2. 🆕 **Include Untracked Files**

By default, `git stash` ignores untracked files.
To stash them as well:

```bash
git stash -u
```

or

```bash
git stash --include-untracked
```

To also include ignored files (rarely needed):

```bash
git stash -a
```

or

```bash
git stash --all
```

---

### 3. 📜 **List All Stashes**

```bash
git stash list
```

Output example:

```
stash@{0}: WIP on main: 34a9f12 Added login validation
stash@{1}: On dev: WIP on API refactor
```

Each stash has:

* An index (like `{0}`, `{1}`)
* The branch it was created on
* The commit reference

---

### 4. 🎒 **Apply a Stash**

To reapply the most recent stash:

```bash
git stash apply
```

To apply a specific stash:

```bash
git stash apply stash@{2}
```

> ⚠️ `apply` does **not delete** the stash from the stash list.
> If you want to both apply and remove it, use `pop`.

---

### 5. 🚀 **Apply and Remove a Stash**

```bash
git stash pop
```

or for a specific one:

```bash
git stash pop stash@{1}
```

This reapplies the changes and then **deletes** the stash entry.

---

### 6. ❌ **Delete a Specific Stash**

```bash
git stash drop stash@{0}
```

Removes that particular stash entry.

---

### 7. 🧹 **Clear All Stashes**

```bash
git stash clear
```

Deletes **all** stashed entries.
⚠️ Use carefully — cannot be undone!

---

### 8. 🔍 **View Stashed Changes**

To see what’s inside a stash:

```bash
git stash show
```

To see a detailed diff:

```bash
git stash show -p
```

---

### 9. 🪄 **Create a Branch from a Stash**

If your stashed work is large and you want to isolate it:

```bash
git stash branch fix-login-bug stash@{0}
```

This will:

1. Create a **new branch** (`fix-login-bug`)
2. **Apply** the stash on it
3. **Remove** the stash entry automatically

---

## 🧠 **Internals**

* Each stash is stored as **two commits** internally:

  * One for the **working directory changes**
  * One for the **staged changes**
* These are stored in `.git/refs/stash` and linked as a stack structure.

---

## ⚡ **Example Workflow**

Let’s say you’re on `main` working on a new feature:

```bash
# 1️⃣ Make some changes
nano app.py

# 2️⃣ Temporarily save your work
git stash save "WIP: feature update"

# 3️⃣ Switch branch safely
git switch bugfix-branch

# 4️⃣ Work and commit there
git commit -m "Fixed production bug"

# 5️⃣ Come back and restore your feature work
git switch main
git stash pop
```


## 🧩 **Real-World Use Cases**

| Scenario                                             | Command to Use                     | Why                                       |
| ---------------------------------------------------- | ---------------------------------- | ----------------------------------------- |
| Need to switch branches but have uncommitted changes | `git stash`                        | Keeps your work safe and allows switching |
| Want to stash new untracked files too                | `git stash -u`                     | Includes files not yet added              |
| Want to test a different feature quickly             | `git stash save "temp changes"`    | Temporarily store ongoing code            |
| Want to recover changes later                        | `git stash list` + `git stash pop` | Brings back stashed work                  |
| Want to move stashed work to a new branch            | `git stash branch`                 | Creates an isolated workspace             |

---

## 🧾 **Key Differences: `stash apply` vs `stash pop`**

| Command           | Reapplies Changes | Removes Stash | Use Case                                  |
| ----------------- | ----------------- | ------------- | ----------------------------------------- |
| `git stash apply` | ✅ Yes             | ❌ No          | When you want to keep the stash for reuse |
| `git stash pop`   | ✅ Yes             | ✅ Yes         | When you’re done with that stash          |

---

## 🧠 **Pro Tips**

* Use meaningful stash messages (`-m "WIP: Login page update"`) for easier tracking.
* Use `git stash show -p > patch.diff` to export stashed changes.
* Avoid excessive stashing — instead, commit to a temp branch if it’s long-term work.
* Use `git stash --keep-index` if you want to stash only unstaged changes.

---

## 🏁 **Summary**

| Action                   | Command                        |
| ------------------------ | ------------------------------ |
| Save work                | `git stash`                    |
| Save with message        | `git stash push -m "message"`  |
| Include untracked files  | `git stash -u`                 |
| List stashes             | `git stash list`               |
| Apply latest stash       | `git stash apply`              |
| Apply and remove stash   | `git stash pop`                |
| Delete specific stash    | `git stash drop stash@{n}`     |
| Delete all stashes       | `git stash clear`              |
| Create branch from stash | `git stash branch branch_name` |

---

Would you like me to create a **diagram** showing how `git stash` moves changes between working directory, staging area, and stash stack? It’s a great visual addition for your “Zero-to-Hero” repo.


## 9. Reset vs Revert

### `git reset`

* Moves `HEAD` (current branch pointer) to a specific commit.
* **Types:**

  * `--soft` → keeps changes staged.
  * `--mixed` → keeps changes unstaged (default).
  * `--hard` → discards changes completely.

Example:

```bash
git reset --hard HEAD~2   # remove last 2 commits
```

⚠️ **Dangerous if already pushed.**

---

### `git revert`

* Safely undo changes by creating a **new commit** that reverses a previous one.
* Preserves history (good for shared repos).

Example:

```bash
git revert <commit_hash>
```

---

## 📝 Key Takeaways

* Git is a **DVCS** → every developer has the full history.
* **Workflow:** Working Dir → Staging → Local Repo → Remote Repo.
* **Branching** enables parallel development.
* **Merge** = safe, **Rebase** = clean but risky.
* **Reset** rewrites history, **Revert** preserves it.

---
