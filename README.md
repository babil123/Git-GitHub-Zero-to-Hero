
# Git
<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/git.png" alt="Banner" />

---

## 1. What is a Version Control System (VCS)?

* A **Version Control System** is software that records changes to files over time so you can recall specific versions later.
* Think of it as a **time machine for your project**.
* Without VCS, you’d manually create copies like `project_v1`, `project_final`, `project_final_final`, which quickly becomes chaotic.

### Benefits

* **Collaboration** – multiple developers can work together without overwriting each other’s changes.
* **History Tracking** – see who changed what, when, and why.
* **Rollback** – return to a previous stable version when needed.
* **Branching** – experiment with features without affecting the main code.


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

<img src="https://github.com/bhuvan-raj/Git-GitHub-Zero-to-Hero/blob/main/assets/gitarchitecture.webp" alt="Banner" />


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

### Analogy:

* `git diff` tells you: **"What's on my desk that I haven't put in the staging area yet?"** (Unstaged changes).
* `git diff --staged` tells you: **"What's in the staging area that is ready to be committed and is different from the last shipped box?"** (Staged changes).


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

👉 Bubu, do you want me to also create a **visual Git workflow diagram + branching strategy diagrams** (like Gitflow vs GitHub Flow) to make this a complete teaching resource for your students?
