# Git Breakdown: Beginner → Pro

## Core Concept
Git = Version Control System (tracks file changes, enables collaboration)

---

## 1. Getting Started

### Beginner
| Concept           |           What It Means |
|-------------------|---------------------------------|
| Version Control   | Save snapshots of your project at different points |
| Repository (repo) | A folder that Git tracks |
| Commit            | A saved snapshot with a message describing changes |

### Pro
| Concept           | What It Means |
|-------------------|---------------|
| VCS Types         | Local → Centralized (SVN) → Distributed (Git) |
| SHA-1             | 40-char hash that uniquely identifies each commit |
| Snapshots         | Git stores differences; GitHub-style stores full file snapshots |

---

## 2. Git Basics

### Beginner
```bash
# Setup
git init                   --->       # Start tracking a project
git clone <url>            --->     # Copy a remote repo locally

# Daily Work
git status                  --->      # What changed?
git add <file>                    # Stage a file for commit
git commit -m "message"           # Save changes
git log                           # View history

# Remote
git pull                          # Get latest changes
git push                          # Send changes to remote
```

### Pro
| Command                    | Purpose |
|----------------------------|---------|
| `git init --bare`          | Create repo without working directory (server) |
| `git add -A` / `git add .` | Stage all changes |
| `git commit -am "msg"`     | Add + commit tracked files only |
| `git diff --staged`        | See staged changes |
| `git restore --staged <file>` | Unstage |
| `git restore <file>`       | Discard unstaged changes |
| `git checkout -- <file>`   | Revert file to last commit |
| `git reset --hard <commit>`| Wipe to specific commit |
| `git reflog`               | Recovery from bad resets |

---

## 3. Branching

### Beginner
```bash
git branch                        # List branches
git branch <name>                 # Create branch
git checkout <branch>            # Switch to that specific branch
git checkout -b <name>            # Create + switch to the branch
git merge <branch>               # Merge branch into current
git branch -d <branch>           # Delete branch
```

### Pro
| Command | Purpose |
|---------|---------|
| `git checkout -b <branch>` | Create and switch |
| `git rebase <branch>` | Rewrite history, linear sequence |
| `git merge --no-ff` | Force merge commit |
| `git cherry-pick <commit>` | Copy specific commit |
| `git stash` | Temporarily save uncommitted work |
| `git stash pop` | Restore stashed work |
| `git worktree` | Multiple working directories |

---

## 4. Remote & Collaboration

### Beginner
```bash
git remote -v                     # Show remotes
git fetch                         # Download without merging
git pull = fetch + merge          # Get and integrate
git push                          # Upload commits
```

### Pro
| Command | Purpose |
|---------|---------|
| `git remote add origin <url>` | Add remote |
| `git push -u origin <branch>` | Set upstream |
| `git fetch --all` | Fetch all remotes |
| `git pull --rebase` | Fetch + rebase (cleaner history) |
| `git push --force` | Overwrite remote (dangerous) |
| `git fetch + git reset --hard origin/main` | Hard reset to remote |

---

## 5. Advanced Tools

### Beginner
```bash
git tag v1.0                      # Create tag (release)
git tag                           # List tags
git tag -d v1.0                   # Delete local tag
```

### Pro
| Command | Purpose |
|---------|---------|
| `git tag -a v1.0 -m "msg"` | Annotated tag |
| `git tag -a v1.0 <commit>` | Tag past commit |
| `git push origin v1.0` | Push tag |
| `git tag -d v1.0 && git push origin :refs/tags/v1.0` | Delete remote tag |
| `git revert <commit>` | Create new commit that undoes previous |
| `git reset --soft HEAD~1` | Undo commit, keep changes staged |
| `git reset --mixed HEAD~1` | Undo commit, keep changes unstaged |
| `git reset --hard HEAD~1` | Undo commit, discard changes |

---

## 6. History & Debugging

### Beginner
```bash
git log --oneline                 # Compact history
git log --graph --oneline         # Visual branch history
git show <commit>                 # View commit details
```

### Pro
| Command | Purpose |
|---------|---------|
| `git log -p` | Show diffs |
| `git log --author="name"` | Filter by author |
| `git log --since="2024-01-01"` | Filter by date |
| `git log -S "string"` | Search for string addition/removal |
| `git log --grep="msg"` | Search commit messages |
| `git blame <file>` | Who changed what line |
| `git bisect` | Binary search for buggy commit |
| `git grep "text"` | Search working directory |

---

## 7. Branching Workflows

### Beginner
- **Main**: Production code
- **Feature branch**: Work on new features

### Pro
| Workflow | Description |
|----------|-------------|
| **Feature Branch** | Each feature = branch → merge to main |
| **Gitflow** | main + develop + feature/release/hotfix branches |
| **Forking** | Open source: fork repo → PR to original |
| **Trunk-based** | Short-lived branches, frequent integration |

---

## 8. Git Internals (Pro Only)

```
.git/
├── objects/     # Blob (file content), Tree (files), Commit (snapshot)
├── refs/        # Branch and tag pointers
├── HEAD         # Current branch
├── index        # Staging area metadata
└── logs/        # Reference history
```

| Command | Purpose |
|---------|---------|
| `git cat-file -p <hash>` | View object content |
| `git ls-tree <tree>` | List tree contents |
| `git gc` | Garbage collection, pack objects |
| `git fsck` | Verify object integrity |

---

## 9. First-Time Setup (Pro Only)

```bash
# Identity
git config --global user.name "Your Name"
git config --global user.email "email@example.com"

# Editor
git config --global core.editor vim
git config --global core.editor code  # VS Code

# Default branch name
git config --global init.defaultBranch main

# Merge strategy
git config --global pull.rebase false

# Useful aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.last 'log -1 HEAD'
git config --global alias.lg "log --oneline --graph --decorate"

# List all config
git config --list
git config --global --list
```

---

## 10. Interactive Staging (Pro)

### Interactive Mode
```bash
git add -i           # Interactive staging
git add --interactive

# Commands in interactive mode:
# s - status, u - update, r - revert, a - add untracked
# p - patch (partial staging), d - diff, q - quit
```

### Partial File Staging
```bash
git add -p           # Stage specific hunks
git add --patch      # Interactively select hunks

# Options for each hunk:
# y - stage, n - skip, a - stage + remaining, d - skip + remaining
# s - split into smaller hunks, e - edit manually, ? - help
```

---

## 11. Stashing & Cleaning (Pro)

### Stashing
```bash
git stash                       # Save uncommitted work
git stash push                  # Same (preferred)
git stash list                  # View stashes
git stash pop                   # Apply + delete latest stash
git stash apply                 # Apply (keep stash)
git stash apply stash@{2}       # Apply specific stash
git stash drop                  # Delete latest stash
git stash drop stash@{0}        # Delete specific stash
git stash clear                 # Delete all stashes

# Advanced stashing
git stash --keep-index          # Keep staged changes too
git stash -u                    # Include untracked files
git stash -a                    # Include ignored files
git stash --patch               # Interactively choose what to stash

# Create branch from stash
git stash branch <name>         # New branch with stashed work
```

### Cleaning
```bash
git clean -n                     # Dry run (show what would be removed)
git clean -f                    # Remove untracked files
git clean -fd                   # Remove files + directories
git clean -fdx                  # Remove everything including ignored
git clean -i                    # Interactive mode
```

---

## 12. Git Hooks (Pro Only)

### Common Client Hooks
| Hook | When It Runs | Common Use |
|------|-------------|-------------|
| `pre-commit` | Before commit msg | Lint, whitespace checks |
| `prepare-commit-msg` | After default msg | Auto-fill templates |
| `commit-msg` | After msg entered | Validate commit format |
| `post-commit` | After commit | Notifications |
| `pre-push` | During push | Run tests, check branches |
| `post-checkout` | After checkout | Setup environment |
| `post-merge` | After merge | Restore permissions |

### Server-Side Hooks
| Hook | When It Runs |
|------|---------------|
| `pre-receive` | Before refs updated (reject push) |
| `update` | Per-branch check |
| `post-receive` | After push complete (notifications) |

```bash
# Location: .git/hooks/
# Enable: rename script (remove .sample), make executable
# Example: pre-commit -> make executable
```

---

## 13. Advanced Merging (Pro)

### Conflict Resolution
```bash
git merge --abort               # Abort merge
git merge --continue           # After resolving

# Ignore whitespace
git merge -Xignore-space-change <branch>
git merge -Xignore-all-space <branch>

# View conflict
git diff                       # What's still conflicting
git diff --ours                # vs our changes
git diff --theirs              # vs their changes
git diff --base                # vs common ancestor
```

### Manual File Merge
```bash
git show :1:file > common.rb   # Get base version (stage 1)
git show :2:file > ours.rb     # Get our version (stage 2)
git show :3:file > theirs.rb  # Get their version (stage 3)

git merge-file -p ours.rb common.rb theirs.rb > file
```

### Merge Strategies
```bash
git merge -s ours <branch>     # Fake merge (keep current code)
git merge -Xours <branch>      # Prefer ours on conflict
git merge -Xtheirs <branch>    # Prefer theirs on conflict
git merge -s recursive -Xsubtree=<dir> <branch>  # Subtree merge
```

### Undoing Merges
```bash
git reset --hard HEAD~         # Reset (local only!)
git revert -m 1 HEAD           # Reverse merge commit
```

---

## 14. Rewriting History (Pro - Local Only!)

### Changing Last Commit
```bash
git commit --amend                    # Change message
git commit --amend --no-edit          # Amend without message
git commit --amend -m "new message"    # Change message + content
git commit --amend --date="2024-01-01" # Change date
```

### Interactive Rebase
```bash
git rebase -i HEAD~3           # Edit last 3 commits
git rebase -i 0b1d4f          # Edit from specific commit

# In rebase editor:
# p - pick   (keep as-is)
# r - reword (change message)
# e - edit   (stop to amend)
# s - squash (merge into previous)
# f - fixup  (like squash, discard message)
# d - drop   (remove commit)
# x - exec   (run shell command)
```

### Squashing Commits
```bash
# Change "pick" to "squash" for commits to merge:
pick abc123 First commit
squash def5678 Second commit
squash ghi9012 Third commit
# All three become one commit
```

### Splitting Commits
```bash
# Mark commit as "edit", then:
git reset HEAD^
git add file1 && git commit -m "first"
git add file2 && git commit -m "second"
git rebase --continue
```

### Nuclear Options
```bash
# Remove file from entire history
git filter-branch --tree-filter 'rm -f file.txt' HEAD

# Change email globally
git filter-branch --commit-filter '
  if [ "$GIT_AUTHOR_EMAIL" = "old@email" ]; then
    GIT_AUTHOR_EMAIL="new@email"; git commit-tree "$@";
  else git commit-tree "$@"; fi' HEAD

# Note: git-filter-repo is recommended over filter-branch
```

### DANGER ZONE
- NEVER rewrite public/shared history
- NEVER rebase pushed commits
- ALWAYS backup before destructive operations
- Use `git reflog` to recover from mistakes

---

## 15. Submodules (Pro)

```bash
# Add submodule
git submodule add <url> <path>
git submodule add https://github.com/user/repo.git libs/common

# Clone with submodules
git clone --recursive <url>
git submodule update --init --recursive

# Working with submodules
git submodule update --remote            # Update submodules
git submodule update --remote --merge    # Update + merge
git submodule deinit -f <path>           # Remove submodule
git rm <path>                            # Remove from index
rm -rf <path>                            # Remove from filesystem

# Run command in all submodules
git submodule foreach 'git pull'
git submodule foreach 'npm install'
```

---

## 16. Git Attributes (Pro)

```bash
# .gitattributes - control file behavior
# Example .gitattributes:
*.txt text=auto
*.sh executable
*.jpg binary
*.png binary
*.pdf binary
*.zip binary
*.java diff=java
*.py diff=python

# Custom diff drivers
[diff "java"]
    xfuncname = "^\\[.*\\]"
```

---

## Quick Reference

| Action | Command |
|--------|---------|
| Start repo | `git init` |
| Clone | `git clone <url>` |
| Check status | `git status` |
| Stage | `git add <file>` |
| Stage all | `git add -A` or `git add .` |
| Commit | `git commit -m "msg"` |
| Add + commit | `git commit -am "msg"` |
| View history | `git log --oneline` |
| View diff | `git diff` |
| Create branch | `git checkout -b <name>` |
| Switch branch | `git checkout <name>` |
| Merge | `git merge <branch>` |
| Rebase | `git rebase <branch>` |
| Pull | `git pull` |
| Push | `git push` |
| Stash | `git stash` |
| Stash pop | `git stash pop` |
| Undo staged | `git restore --staged <file>` |
| Undo changes | `git restore <file>` |
| Reset to remote | `git fetch && git reset --hard origin/main` |


*Reference based on Pro Git Book - https://git-scm.com/book/*