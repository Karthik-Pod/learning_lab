# 01 – Git basics

**Goal:** use Git without notes: branch, commit, inspect, undo, resolve a
conflict, and get work merged through a pull request.

**Warm-up (before you start):** [learngitbranching.js.org](https://learngitbranching.js.org),
"Introduction Sequence" levels 1–4.

Work in PowerShell inside your `learning_lab` folder. After every command, run
`git status` and read what it says – that habit is half of knowing Git.

---

## Exercise 1 – Small commits and history

1. Create a branch: `git checkout -b practice/commits`
2. Create `01-git-basics/notes.md` with one line: what a commit is, in your words.
3. `git add 01-git-basics/notes.md` then `git commit -m "Add notes on commits"`
4. Add a line about what a branch is. Commit again.
5. Add a line about what staging (`git add`) is. Commit again.
6. Look at your history: `git log --oneline`

✅ You see 3 separate commits with clear messages.

**Why:** small commits with clear messages are easy to review and easy to undo.

---

## Exercise 2 – See what changed

1. Add a fourth line to `notes.md`, but don't stage it.
2. `git diff` – shows changes **not yet staged**.
3. `git add 01-git-basics/notes.md`
4. `git diff` again – empty! Now try `git diff --staged`.
5. Commit it.

✅ You can explain the difference between `git diff` and `git diff --staged`.

---

## Exercise 3 – Undo things (safely)

| Situation | Command |
|---|---|
| Throw away unstaged changes to a file | `git restore <file>` |
| Unstage a file (keep the change) | `git restore --staged <file>` |
| Undo a commit that is already pushed | `git revert <commit-id>` |

1. Write some nonsense into `notes.md`, then throw it away with `git restore`.
2. Write nonsense again, `git add` it, then unstage it with `git restore --staged`,
   then throw it away.
3. Make a bad commit on purpose, then undo it with `git revert <id>`
   (find the id with `git log --oneline`). Look at the log afterwards.

✅ You know which undo to use, and why `revert` adds a new commit instead of deleting one.

---

## Exercise 4 – Make and fix a merge conflict

Conflicts happen when two branches change the **same line**. Make one on purpose:

1. `git checkout main` and create `01-git-basics/conflict.md` with one line:
   `My favourite language is Python.` – commit it.
2. `git checkout -b practice/branch-a` – change the line to `... is Rust.` – commit.
3. `git checkout main` then `git checkout -b practice/branch-b` – change the
   same line to `... is Dart.` – commit.
4. `git checkout practice/branch-a` then `git merge practice/branch-b`
5. Git reports a **CONFLICT**. Open `conflict.md` – you'll see:

   ```
   <<<<<<< HEAD
   My favourite language is Rust.
   =======
   My favourite language is Dart.
   >>>>>>> practice/branch-b
   ```

6. Edit the file to the final text you want, delete the `<<<<<<<`, `=======`,
   `>>>>>>>` lines, save.
7. `git add 01-git-basics/conflict.md` then `git commit` (accept the default message).

✅ You resolved a conflict without panicking. In team projects, this is the moment
most people get stuck.

---

## Exercise 5 – The full pull-request flow

This is exactly what you did for PR #24 in the SDE project – now alone, start to finish.

1. `git checkout main` then `git pull`
2. `git checkout -b practice/first-pr`
3. Add a short "What I learned" section to `notes.md`. Commit.
4. `git push -u origin practice/first-pr`
5. On GitHub: open the pull request (base: `main`), write a 2-line description.
6. Review your own PR in **Files changed** – leave one comment on a line.
7. Click **Merge pull request**, then **Delete branch**.
8. Back in PowerShell: `git checkout main` then `git pull`
9. Clean up locally: `git branch -d practice/first-pr`

✅ Your change is on `main`, the branch is gone, and your local `main` is up to date.

---

## Done when

- [ ] I can do exercises 1–5 again **without looking at this file**
- [ ] I wrote a learning-log entry about Git
- [ ] I ticked `01-git-basics` in the README

## Cheat sheet

| Command | What it does |
|---|---|
| `git status` | What's changed, what's staged, which branch I'm on |
| `git checkout -b <name>` | Create a branch and switch to it |
| `git checkout <name>` | Switch to an existing branch |
| `git add <file>` | Stage a file for the next commit |
| `git commit -m "msg"` | Save staged changes as a commit |
| `git log --oneline` | Short history |
| `git diff` / `git diff --staged` | Unstaged / staged changes |
| `git push -u origin <branch>` | Upload a new branch to GitHub |
| `git pull` | Download and merge the latest changes |
| `git merge <branch>` | Merge another branch into the current one |
| `git branch -d <name>` | Delete a merged local branch |
