# 01 – Git & GitHub

**Goal:** use Git and GitHub confidently, alone and in a team, without notes.

**How to use this guide**
- Go through the topics **in order**. Each one has:
  - **What** – the idea in plain words
  - **Why it matters** – where you'll need it
  - **Try it** – steps to do yourself, in the `playground/` folder of this repo
  - **You've got it when** – how to know you're done
- Run commands in PowerShell inside `C:\Users\karth\learning_lab`.
- Edit files in VS Code (or Notepad) – not with commands.
- After **every** command, run `git status` and read it. That habit alone teaches you half of Git.
- Visual warm-up that helps a lot: [learngitbranching.js.org](https://learngitbranching.js.org)
  ("Introduction Sequence"). Do it alongside topics 4–6.

---

## Part A – Git on your own laptop

### Topic 1 – Repositories and the 4 places

**What:** A *repository* (repo) is a project folder whose history Git tracks.
Your work moves between 4 places:

```
working folder ──git add──▶ stage ──git commit──▶ local repo ──git push──▶ GitHub (remote)
     ◀───────────────────────────── git pull ─────────────────────────────────┘
```

| Place | Meaning |
|---|---|
| Working folder | The files you see and edit |
| Stage | Changes you've selected for the next commit |
| Local repo | Saved snapshots (commits) on your laptop |
| Remote | The copy on GitHub, shared with others |

**Why it matters:** every Git command moves work between these places. If you
know which place your change is in, Git stops being confusing.

**Try it**
1. `git status` in your repo – which branch are you on? Is anything changed?
2. Create the folder `01-git-github/playground/` and a file `hello.md` in it with one line.
3. `git status` → the file is **untracked** (in the working folder only).

**You've got it when:** you can draw the 4 places from memory and say which
command moves work between each.

---

### Topic 2 – Staging and committing

**What:** `git add` puts a change on the stage. `git commit` saves everything on
the stage as one snapshot with a message. You choose **what** goes in each commit.

**Why it matters:** this is how you kept the generated Flutter files out of
PR #24 – you staged only your 5 files.

**Try it**
1. `git checkout -b practice/commits`
2. `git add 01-git-github/playground/hello.md` → `git status` (green = staged)
3. `git commit -m "Add hello file"`
4. Add a second line to `hello.md` **and** create `other.md`.
5. Stage **only** `hello.md`, commit it. Then stage and commit `other.md` separately.

**You've got it when:** you can make two separate commits out of changes to two
files, on purpose.

---

### Topic 3 – Reading history and changes

**What:** Git can show what changed and when.

| Command | Shows |
|---|---|
| `git log --oneline` | List of commits, short |
| `git show <commit-id>` | What one commit changed |
| `git diff` | Changes **not yet staged** |
| `git diff --staged` | Changes **staged** for the next commit |

**Why it matters:** before every commit, `git diff --staged` shows exactly what
you're about to save – it catches mistakes before teammates see them.

**Try it**
1. `git log --oneline` – find your two commits from Topic 2.
2. `git show <id>` on one of them.
3. Change a line in `hello.md`. Run `git diff`. Stage it. Run `git diff` again
   (empty!) and then `git diff --staged`. Commit.

**You've got it when:** you can explain the difference between `git diff` and
`git diff --staged`.

---

### Topic 4 – Branches

**What:** A branch is a separate line of work. Commits on it don't affect other
branches until you merge. `main` is the default branch.

```
main:      A ── B
                 \
practice/x:       C ── D     ← your work, main is untouched
```

**Why it matters:** in a team, everyone works on their own branch so nobody
breaks the shared code. That's why you made `create_group_page`.

| Command | Does |
|---|---|
| `git branch` | List branches (`*` = current) |
| `git checkout -b <name>` | Create a branch and switch to it |
| `git checkout <name>` | Switch to an existing branch |
| `git branch -d <name>` | Delete a merged branch |

**Try it**
1. `git checkout main` – look in `playground/`: your files from Topic 2 are **gone**.
2. `git checkout practice/commits` – they're **back**.
3. `git branch` – see both branches.

**You've got it when:** you understand why files "disappear" when switching
branches (they belong to the other branch's history, they aren't deleted).

---

### Topic 5 – Merging

**What:** Merging brings commits from one branch into another.
- **Fast-forward:** the target branch had no new commits, so Git just moves it forward.
- **Merge commit:** both branches have new commits, so Git creates a commit that joins them.

**Why it matters:** every PR you merge on GitHub is a merge.

**Try it**
1. `git checkout main` → `git merge practice/commits` → read the output: "Fast-forward".
2. Make branch `practice/a` from main, commit a change to `hello.md`.
3. Switch to main, commit a change to `other.md` (a *different* file).
4. `git merge practice/a` → Git makes a **merge commit** (an editor may open: save and close it).
5. `git log --oneline --graph` – see the two lines join.

**You've got it when:** you can say whether a merge will be fast-forward before running it.

---

### Topic 6 – Merge conflicts

**What:** A conflict happens when two branches change the **same lines**. Git
can't choose, so it asks you.

**Why it matters:** in team projects this is where people panic. It's just a
file you edit.

**Try it**
1. On `main`, create `playground/conflict.md` with `My favourite language is Python.` – commit.
2. `git checkout -b practice/rust` – change it to `... is Rust.` – commit.
3. `git checkout main` – change the same line to `... is Dart.` – commit.
4. `git merge practice/rust` → **CONFLICT**. Open the file:

   ```
   <<<<<<< HEAD
   My favourite language is Dart.
   =======
   My favourite language is Rust.
   >>>>>>> practice/rust
   ```
   Top part = your current branch. Bottom part = the branch you're merging in.
5. Edit it to what you want, delete the three marker lines, save.
6. `git add 01-git-github/playground/conflict.md` → `git commit`.

**You've got it when:** you can resolve a conflict calmly and explain what the
markers mean.

---

### Topic 7 – Undoing mistakes

**What:** Different mistakes need different undos.

| Mistake | Fix | Safe? |
|---|---|---|
| Bad edits, not staged | `git restore <file>` | Deletes those edits |
| Staged by accident | `git restore --staged <file>` | Keeps the edits |
| Typo in the last commit message (not pushed) | `git commit --amend -m "new msg"` | Only before pushing |
| A pushed commit was wrong | `git revert <id>` | ✅ Always safe |

**Why it matters:** `revert` adds a **new** commit that undoes an old one, so
history isn't rewritten – that's why it's the safe choice on shared branches.

**Try it**
1. Write nonsense in `hello.md` → throw it away with `git restore`.
2. Write nonsense, `git add` it → unstage with `git restore --staged` → throw away.
3. Commit with a typo in the message → fix it with `--amend`.
4. Make a bad commit → undo with `git revert <id>` → look at `git log --oneline`.

**You've got it when:** for any mistake, you know which undo to pick.

---

### Topic 8 – Remotes: push, pull, fetch

**What:** The remote (`origin`) is the GitHub copy.

| Command | Does |
|---|---|
| `git push -u origin <branch>` | Upload a new branch (first time) |
| `git push` | Upload new commits (after `-u`) |
| `git fetch` | Download info about GitHub's state, change nothing locally |
| `git pull` | `fetch` + merge into your current branch |

**Why it matters:** `git status` only compares with what your laptop **last
saw** from GitHub – you saw this when it said "up to date" and `git pull`
still downloaded your log edit.

**Try it**
1. Push your `main`: `git push`.
2. On GitHub, edit `playground/hello.md` directly and commit there.
3. Locally: `git status` (says up to date!) → `git fetch` → `git status` (now "behind by 1") → `git pull`.
4. Now the rejected-push case: edit a file on GitHub again, **don't pull**, make a
   local commit, `git push` → **rejected**. Fix it with `git pull`, then `git push`.

**You've got it when:** a rejected push doesn't scare you – you know to pull first.

---

### Topic 9 – `.gitignore`

**What:** A file listing things Git should never track: build output, secrets,
editor settings, large data.

**Why it matters:** the generated Flutter files in SDE kept appearing in
`git status`. In your own projects, `.gitignore` prevents that – and stops you
from ever pushing passwords or API keys.

**Try it**
1. Create `playground/secret.txt` and a folder `playground/build/` with a file in it.
2. `git status` → both show up.
3. Create `.gitignore` in the repo root:
   ```
   secret.txt
   build/
   ```
4. `git status` → they're gone. Commit the `.gitignore`.

**You've got it when:** you add a `.gitignore` as the first thing in every new project.

---

### Topic 10 – Stash

**What:** `git stash` puts unfinished changes aside so you can switch branches;
`git stash pop` brings them back.

**Why it matters:** you're halfway through something and a teammate asks you to
check their branch. Stash, switch, check, switch back, pop.

**Try it**
1. Edit `hello.md`, don't commit.
2. `git stash` → `git status` is clean.
3. Switch to another branch and back.
4. `git stash pop` → your edit is back.

**You've got it when:** you can switch branches mid-work without committing half-done changes.

---

## Part B – GitHub and teamwork

### Topic 11 – Pull requests and code review

**What:** A PR asks: "please merge my branch into this one". Others review the
changes, comment on lines, approve or request changes.

**Why it matters:** this is how every team project works – you've done both
sides already (PR #24, and reviewing Matej's #22).

**Try it**
1. Branch `practice/first-pr`, change something in `playground/`, push.
2. Open a PR (base: `main`), write a description: **what** and **why**.
3. In **Files changed**, comment on one line, like a reviewer would.
4. Push one more commit to the same branch → see the PR update automatically.
5. Merge, delete the branch, `git checkout main`, `git pull`, `git branch -d practice/first-pr`.

**You've got it when:** you can do the full cycle without this guide.

---

### Topic 12 – Issues and linking work

**What:** Issues are tasks or bugs. Every issue and PR gets a number (shared counter).
Writing `#5` anywhere links to it. `Closes #5` in a PR description closes the issue
when the PR merges **into the default branch**.

**Why it matters:** this is how your SDE team assigns and tracks work (#19 was yours).

**Try it**
1. Create an issue in this repo: "Practice: add notes on issues".
2. Branch, add `playground/issues.md`, push, open a PR with `Closes #<number>`.
3. Merge → the issue closes by itself.

**You've got it when:** you can connect an issue, a branch and a PR.

---

### Topic 13 – Forks

**What:** A fork is your own copy of someone else's repo on GitHub. You change
your fork, then open a PR back to the original.

**Why it matters:** this is how you contribute to repos where you have **no write
access** – open-source projects, research code from other labs. (In SDE you're a
collaborator, so you push branches directly instead.)

**Try it**
1. Fork any small public repo (or a friend's).
2. Clone **your fork**, make a branch, push to your fork.
3. Look at how GitHub offers "Contribute → Open pull request" to the original.
   (You don't have to actually submit it.)

**You've got it when:** you can explain when to fork and when to just branch.

---

### Topic 14 – Keeping a branch up to date in a team

**What:** While you work on your branch, `main` (or `developer`) moves on.
Before your PR merges, you bring those changes into your branch:

```
git checkout main
git pull
git checkout my-branch
git merge main
```

**Why it matters:** in SDE, Matej's branch was 8 commits behind `developer` and
GitHub said your stack was "out of date". Merging the latest base into your
branch fixes that, and lets **you** solve any conflicts instead of the reviewer.

**Try it**
1. Branch `practice/feature`, commit a change.
2. Switch to `main`, commit a different change (simulating a teammate).
3. Back on `practice/feature`: `git merge main`.
4. `git log --oneline --graph` – your branch now contains both.

**You've got it when:** you update your branch before asking for a review.

---

### Topic 15 – Good commit messages

**What:** A commit message should say **what the commit does**, in the
imperative, short: `Add create group page`, `Fix date format in API client`.

| Bad | Good |
|---|---|
| `update` | `Add validation for end time` |
| `fixed stuff` | `Fix 404 on create_activity: send JSON header` |
| `asdf` | `Remove unused counter demo from main.dart` |

**Why it matters:** in six months, `git log` is the only explanation of why code
changed – for teammates and for you.

**Try it**
1. `git log --oneline` in this repo – rate your own messages.
2. For your next 10 commits, write messages that someone else would understand.

**You've got it when:** your `git log` reads like a list of clear changes.

---

## Done with this area when

- [ ] I can do topics 1–11 **without looking at this guide**
- [ ] I've resolved at least two conflicts myself
- [ ] I ticked the Git & GitHub topics in the main README
- [ ] I wrote log entries about what was hardest

## Cheat sheet

| Command | What it does |
|---|---|
| `git status` | What changed, what's staged, which branch |
| `git add <file>` | Stage a file |
| `git commit -m "msg"` | Save staged changes |
| `git log --oneline --graph` | History as a picture |
| `git diff` / `git diff --staged` | Unstaged / staged changes |
| `git checkout -b <name>` | New branch + switch |
| `git checkout <name>` | Switch branch |
| `git merge <branch>` | Merge a branch into the current one |
| `git restore <file>` | Throw away unstaged edits |
| `git restore --staged <file>` | Unstage |
| `git revert <id>` | Safely undo a pushed commit |
| `git stash` / `git stash pop` | Park / restore unfinished work |
| `git fetch` / `git pull` / `git push` | Sync with GitHub |
| `git branch -d <name>` | Delete a merged branch |
