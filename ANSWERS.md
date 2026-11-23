# Git Mini Exercise: answers

## Part 1: Setup and config
1. Install: `sudo apt install git` (Linux) or `brew install git` (Mac); on Windows, download Git from git-scm.com.
2. Version: `git --version`
3. Identity:
```
git config --global user.name "Your Name"
git config --global user.email "you@example.com"
```

## Part 2: First repository
```
mkdir my-first-repo
cd my-first-repo
git init
touch readme.txt
```

## Part 3: First commit
1. `git status`
2. `git add readme.txt`
3. `git commit -m "Add readme file"`
4. `git log` (or `git log --oneline`)

## Part 4: Make changes
1. Added a second line to `readme.txt`.
2. `git status` shows that `readme.txt` is **modified** but **not staged**: Git sees the change but it is not yet prepared for the next commit.
3. `git add readme.txt` then `git commit -m "Update readme with a second line"`
4. **2 commits.**

## Part 5: Exploration
- `git diff` shows the exact lines changed in files that are not staged yet (`+` for added lines, `-` for removed lines).
- `git log --oneline` shows the history in a compact form: one line per commit, with a short hash and the message.

## Part 6: Branches
1. `git branch`
2. `git branch feature-script`
3. `git switch feature-script` (or `git checkout feature-script`)
4. `git switch -c dev` (or `git checkout -b dev`)
5. `git switch feature-script`
6. `git branch` (the current branch has a `*`) or `git branch --show-current`

## Part 7: Bash script on a branch
`install.sh`:
```bash
#!/bin/bash
echo "Starting installation..."
sudo apt-get update
sudo apt-get install -y git
echo "Installation complete!"
```
Make it executable: `chmod +x install.sh`
Commit: `git add install.sh` then `git commit -m "Add install script"`
History: `git log --oneline` shows 3 commits on this branch.

## Part 8: Merge
1. `git switch main`
2. `ls`: `install.sh` is **not** there, because it was committed only on `feature-script`; `main` has not received it yet.
3. `git merge feature-script`
4. `ls` again: `install.sh` is now in the directory.
5. History: `main` now has the install-script commit. It was a **fast-forward** merge, since `main` had not moved after the branch was created, so the history stays a straight line with no merge commit.
6. `git branch -d feature-script`

## Part 9: Push to GitHub
1. Created the repository on github.com, empty, with no README.
2. Link: `git remote add origin https://github.com/idrissel07/GitExo-Slide26.git`
3. Push: `git push -u origin main`
4. After refreshing, the page shows the files `readme.txt` and `install.sh` and the commit history.

## Part 10: Delete and clone
1. `cd ..`
2. `rm -rf my-first-repo`
3. `git clone https://github.com/idrissel07/GitExo-Slide26.git`
4. `cd GitExo-Slide26` then `ls`: the files are back.

## Part 11: Full workflow practice
Done in the separate repository `bash-installer`: README on `main`, branch `feature-install` with the install script, merge into `main` (with `--no-ff`, so a merge commit appears), branch deleted, then pushed.
```
mkdir bash-installer && cd bash-installer
git init
(create README.md)  git add README.md  git commit -m "Add README explaining the project"
git switch -c feature-install
(add install.sh)  git add install.sh  git commit -m "Add install script"
git switch main
git merge --no-ff feature-install
git branch -d feature-install
git remote add origin <url>   git push -u origin main
```

## Reflection questions
1. Version control keeps the full history, lets you undo mistakes, and lets several people work on the same project.
2. Staging (`git add`) chooses which changes go into the next snapshot; committing (`git commit`) saves that snapshot in the history.
3. Commit when you finish one small, coherent piece of work that runs.
4. `git init` creates a new empty repository; `git clone` copies an existing remote repository, with its history.
5. Good messages explain what changed and why, so you and others can understand the history later.
6. Branches let you develop a feature or fix in isolation, without breaking `main`.
7. Create a branch for any new feature, experiment or bug fix, before merging it back into `main`.
