# Git Quick Reference - Developer Master Guide

> Concise commands for my daily development work. **Keep this handy!**

---

## Daily Workflow

```bash
# Start a new project
git init
git clone <url>

# Check status
git status
git status -s              # Short format

# Stage changes
git add <file>            # Single file
git add .                 # All changes
git add -A                # All including deleted
git add -p                # Interactive patch

# Commit
git commit -m "message"
git commit -am "msg"      # Stage tracked + commit

# View history
git log --oneline
git log --oneline --graph --decorate
git log -p                # With diffs
git log --author="name"
git log --since="2024-01-01"
git log -S "string"       # Search changes

# View differences
git diff                  # Unstaged
git diff --staged         # Staged
git diff HEAD             # All changes
git diff <branch>         # vs branch
git diff --stat           # Summary only
```

---

## Branching

```bash
# List & manage branches
git branch                # Local branches
git branch -r            # Remote branches
git branch -a            # All branches
git branch <name>        # Create
git branch -d <name>    # Delete (safe)
git branch -D <name>    # Delete (force)

# Switch & create
git checkout <branch>   # Switch to branch
git checkout -b <name>  # Create + switch
git switch <branch>     # New syntax
git switch -c <name>    # Create + switch

# Merge
git merge <branch>
git merge --no-ff <branch>  # Force merge commit
git merge --abort           # Cancel merge

# Rebase (rewrite history!)
git rebase <branch>
git rebase -i HEAD~3        # Interactive rebase
git rebase --continue       # After resolving
git rebase --abort          # Cancel rebase
```

---

## Remote Operations

```bash
# Remotes
git remote -v
git remote add origin <url>
git remote remove origin

# Fetch & pull
git fetch                  # Download
git fetch --all            # All remotes
git pull                   # Fetch + merge
git pull --rebase          # Fetch + rebase

# Push
git push
git push -u origin <branch>    # Set upstream
git push --force               # DANGER!
git push --force-with-lease    # Safer force
```

---

## Undo & Recovery

```bash
# Unstage
git restore --staged <file>
git reset HEAD <file>

# Discard changes
git restore <file>
git checkout -- <file>

# Undo commits
git reset --soft HEAD~1     # Keep staged
git reset --mixed HEAD~1    # Keep unstaged (default)
git reset --hard HEAD~1     # DISCARD (danger!)

# Amend last commit
git commit --amend
git commit --amend --no-edit
git commit --amend -m "new msg"

# Revert (safe undo)
git revert <commit>
git revert HEAD~3..HEAD     # Revert range
```

---

## Stashing

```bash
git stash                  # Save work in progress
git stash push            # Same
git stash list            # View stashes
git stash pop             # Apply + delete
git stash apply           # Apply (keep)
git stash apply stash@{2} # Specific stash

# Advanced
git stash -u              # Include untracked
git stash --patch          # Interactive
git stash branch <name>   # Create branch from stash
```

---

## Debugging & Inspection

```bash
# Who changed what
git blame <file>
git blame -L 10,20 <file>  # Specific lines

# Binary search for bugs
git bisect start
git bisect bad
git bisect good <commit>
git bisect reset           # End session

# Search
git grep "text"
git grep -n "text"        # With line numbers
git log --grep="text"     # Search messages

# Show
git show <commit>
git show <commit> --stat  # Summary
```

---

## Tags

```bash
git tag                    # List
git tag <name>             # Lightweight
git tag -a <name> -m "msg" # Annotated
git tag -a <name> <commit> # Tag past commit
git tag -d <name>          # Delete local

# Push tags
git push origin <tag>
git push --tags            # All tags
git push origin :refs/tags/<tag>  # Delete remote
```

---

## Configuration

```bash
# Identity
git config --global user.name "Name"
git config --global user.email "email"

# Editor
git config --global core.editor vim
git config --global core.editor "code --wait"

# Useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.last 'log -1 HEAD'
git config --global alias.unstage 'reset HEAD --'
git config --global alias.lg "log --oneline --graph --decorate"

# View config
git config --list
git config --global --list
git config user.name           # Specific value
```

---

## Advanced

```bash
# Worktree (multiple directories)
git worktree list
git worktree add <path> -b <branch>
git worktree remove <path>

# Cherry-pick
git cherry-pick <commit>
git cherry-pick -n <commit>  # No commit

# Submodules
git submodule add <url> <path>
git submodule update --init
git submodule update --remote

# Interactive staging
git add -i
git add -p

# Clean
git clean -n              # Dry run
git clean -f              # Remove files
git clean -fd             # Remove + dirs
git clean -fdx            # Remove all
```

---

## Emergency Recovery

```bash
# Lost commits? Check reflog
git reflog
git reflog show HEAD
git checkout <commit>     # Go to lost commit

# Recover branch
git branch <name> <commit>

# Find lost commits
git fsck --lost-found

# Check HEAD
git log --walk-reflogs
```

---

## Pro Tips

```bash
# Better log output
git log --pretty=format:"%h %s" --graph
git log --oneline --all --decorate

# Useful flags
-p  = patch (show diff)
--stat = summary
--graph = ASCII graph
--decorate = branches/tags

# Ignore files temporarily
git update-index --assume-unchanged <file>
git update-index --no-assume-unchanged <file>
git ls-files -v | grep '^h'

# Diff branches nicely
git diff main..feature
git log main ^feature  # commits in main not in feature
```

---

## Quick Decision Chart

| Need | Command |
|------|---------|
| Save work temporarily | `git stash` |
| Unstage file | `git restore --staged .` |
| Discard changes | `git restore .` |
| Undo last commit | `git reset --soft HEAD~1` |
| See what's in stash | `git stash list` |
| Force push (careful!) | `git push --force-with-lease` |
| Clean untracked files | `git clean -fd` |
| View file history | `git log -p file.txt` |
| Find bug introduction | `git bisect` |
| Combine last 3 commits | `git rebase -i HEAD~3` |

---

## Common Remote URLs

```bash
# GitHub
git clone https://github.com/user/repo.git
git clone git@github.com:user/repo.git

# GitLab
git clone https://gitlab.com/user/repo.git

# Bitbucket
git clone https://bitbucket.org/user/repo.git
```

---

*Reference based on Pro Git Book - https://git-scm.com/book/*