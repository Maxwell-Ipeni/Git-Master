# Git Breakdown: Beginner → Pro

## Core Concept
Git = Version Control System (tracks file changes, enables collaboration)

---

## 1. Getting Started

### Beginner
| Concept | What It Means |
|---------|---------------|
| Version Control | Save snapshots of your project at different points |
| Repository (repo) | A folder that Git tracks |
| Commit | A saved snapshot with a message describing changes |

### Pro
| Concept | What It Means |
|---------|---------------|
| VCS Types | Local → Centralized (SVN) → Distributed (Git) |
| SHA-1 | 40-char hash that uniquely identifies each commit |
| Snapshots | Git stores differences; GitHub-style stores full file snapshots |

---

## 2. Git Basics

### Beginner
```bash
# Setup
git init                          # Start tracking a project
git clone <url>                   # Copy a remote repo locally

# Daily Work
git status                        # What changed?
git add <file>                    # Stage a file for commit
git commit -m "message"           # Save changes
git log                           # View history

# Remote
git pull                          # Get latest changes
git push                          # Send changes to remote
```

### Pro
| Command | Purpose |
|---------|---------|
| `git init --bare` | Create repo without working directory (server) |
| `git add -A` / `git add .` | Stage all changes |
| `git commit -am "msg"` | Add + commit tracked files only |
| `git diff --staged` | See staged changes |
| `git restore --staged <file>` | Unstage |
| `git restore <file>` | Discard unstaged changes |
| `git checkout -- <file>` | Revert file to last commit |
| `git reset --hard <commit>` | Wipe to specific commit |
| `git reflog` | Recovery from bad resets |

---

## 3. Branching

### Beginner
```bash
git branch                        # List branches
git branch <name>                 # Create branch
git checkout <branch>            # Switch branch
git checkout -b <name>            # Create + switch
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

## Quick Reference

| Action | Command |
|--------|---------|
| Start repo | `git init` |
| Clone | `git clone <url>` |
| Check status | `git status` |
| Stage | `git add <file>` |
| Commit | `git commit -m "msg"` |
| View history | `git log --oneline` |
| Create branch | `git checkout -b <name>` |
| Merge | `git merge <branch>` |
| Pull | `git pull` |
| Push | `git push` |
| Undo staged | `git restore --staged <file>` |
| Undo changes | `git restore <file>` |
