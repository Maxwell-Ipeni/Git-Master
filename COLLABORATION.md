# Git Collaboration Commands

## Starting Work

| Command | Description |
|---------|-------------|
| `git clone <url>` | Copy a remote repository to your local machine |
| `git init` | Initialize a new local repository |

## Basic Snapshotting

| Command | Description |
|---------|-------------|
| `git add <file>` | Stage a specific file for commit |
| `git add .` / `git add -A` | Stage all changes (new, modified, deleted) |
| `git commit -m "message"` | Save staged changes with a message |
| `git commit --amend` | Modify the last commit (message or content) |

## Branching

| Command | Description |
|---------|-------------|
| `git branch` | List local branches |
| `git branch <name>` | Create a new branch |
| `git checkout <branch>` | Switch to an existing branch |
| `git checkout -b <name>` | Create and switch to a new branch |
| `git switch <branch>` | Switch to an existing branch (modern syntax) |
| `git switch -c <name>` | Create and switch to a new branch (modern syntax) |
| `git branch -d <name>` | Delete a branch (safe - fails if unmerged) |
| `git branch -D <name>` | Delete a branch (force) |

## Integrating Changes

| Command | Description |
|---------|-------------|
| `git merge <branch>` | Merge a branch into the current branch |
| `git rebase <branch>` | Reapply commits on top of another branch |
| `git rebase -i HEAD~n` | Interactive rebase to edit, squash, or reorder commits |
| `git cherry-pick <commit>` | Apply a specific commit to the current branch |

## Fetching & Pulling

| Command | Description |
|---------|-------------|
| `git fetch` | Download commits and branches from remote (no merge) |
| `git pull` | Fetch and merge changes from the remote branch |
| `git pull --rebase` | Fetch and rebase instead of merge (cleaner history) |

## Pushing

| Command | Description |
|---------|-------------|
| `git push` | Upload local commits to the remote |
| `git push -u origin <branch>` | Push and set the upstream tracking branch |
| `git push --force` | Overwrite remote with local (dangerous - use with caution) |
| `git push --force-with-lease` | Safer force push - fails if remote changed |

## Remote Management

| Command | Description |
|---------|-------------|
| `git remote -v` | List configured remotes |
| `git remote add origin <url>` | Add a remote |
| `git remote remove <name>` | Remove a remote |

## Temporary Storage

| Command | Description |
|---------|-------------|
| `git stash` | Temporarily save uncommitted changes |
| `git stash pop` | Apply stashed changes and remove from stash list |
| `git stash apply` | Apply stashed changes (keeps them in stash) |
| `git stash list` | View all stashes |

## Collaboration Workflows

| Command | Description |
|---------|-------------|
| `git fetch origin` | Get latest state of remote without merging |
| `git reset --hard origin/main` | Reset local to match remote (DISCARDS local changes) |
| `git pull origin <branch>` | Pull from a specific remote branch |
| `git push origin <branch>` | Push to a specific remote branch |

## Inspection

| Command | Description |
|---------|-------------|
| `git log --oneline --graph --all` | Visual history of all branches |
| `git diff <branch1> <branch2>` | Compare two branches |
| `git log <branch>..<branch>` | Commits in one branch but not another |
| `git show <commit>` | View details of a specific commit |
| `git blame <file>` | Show who changed each line and when |

---

*Reference: https://git-scm.com/book/*