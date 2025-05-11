# 🚀 Git Concepts & Commands Cheatsheet

## Key Repository Terms

### **main (or master)**
- **What is it ?** The default branch name in most Git repositories (like the "trunk" of a tree).
- **Purpose:** Stores the official/production-ready code.

### **origin**
- **What is it ?** The default nickname for your remote repository (usually your fork or clone on GitHub/GitLab).
- **Purpose:** Where you push/pull your own changes.

### **upstream**
- **What is it ?** A nickname for the original repository (if you forked a project).
- **Purpose:** Sync your fork with the original project's updates.

---

## Basic Linux Commands

| Command | Description |
|---------|-------------|
| `ls` | List all files/folders |
| `touch file.txt` | Creates new file |
| `mkdir directory_name` | Make Directory |
| `cd directory_name` | Change Directory |
| `vi file.txt` | Create & open file in vim editor |
| `cat file.txt` | Display file content |
| `rm file.txt` | Remove file |
| `rm -f file.txt` | Force delete (ignores warnings & delete without asking) |
| `rm -rf folder_name` | Recursive delete (delete folders & everything inside a folder) |
| `rm -ri folder_name` | Interactive delete (asks before deleting each file) |

---

## Git Commands

### Basics
```bash
git init                  # Initialize Git repository
ls -a                     # Show hidden files (including .git)
ls .git                   # Show Git directory contents
git status                # Show working tree status
git add .                 # Add all files to staging
git add file.txt          # Add specific file to staging
git commit -m "message"   # Commit with message
git log                   # View commit history
```

### Restore
```bash
git restore --staged file.txt  # Remove file from the staging area (but keeps changes)
git restore file.txt           # Discard working directory changes, use carefully!
```

### Reset
```bash
git reset --soft HEAD~1      # Undo commit, keep changes staged. (HEAD~1 means "one commit before the latest")
git reset --mixed HEAD~1     # Undo commit + unstage changes 
git reset                    # works same as --mixed
git reset --hard HEAD~1      # Completely undo commit + lose changes, use carefully!
```

### Stash
```bash
git stash                         # Temporarily save changes
git stash save "message"          # Stash with description, recommended
git stash list                    # List all stashes
git stash pop                     # Apply & remove latest stash
git stash apply                   # Apply without removing
git stash apply stash@{0}         # Apply specific stash
git stash drop stash@{1}          # Delete specific stash
git stash clear                   # Delete ALL stashes, use carefully!
```

### Remote
```bash
git remote add origin url       # Connect local repo to remote repo
git remote -v                   # View connected remotes
git remote remove origin        # Remove remote connection
```

### Pull
Imp Note: Before coding, always pull the latest changes to avoid conflicts.
```bash
git pull                       # Fetch + merge changes
git pull --rebase              # Instead of a merge commit, it rewinds your changes, applies updates, then replays your work on top.
git pull upstream main         # Pull from original repo's main branch (if forked a repo)
```

### Push
```bash
git push -u origin main       # First-time push (sets upstream)
git push                      # Push to default remote
git push origin main          # Push to main branch
git push origin feature/login # Push to specific branch i.e feature/login
git push origin branch -f     # Force push (use carefully!)
```

### Clone
```bash
git clone url                 # Clone repository
git clone url my_folder       # Clone into custom folder
git clone -b branch_name url  # Clone specific branch
```

### Branch
```bash
git branch                     # List all branches
git branch new_name            # Create new branch
git branch -d branch_name      # Delete branch
git branch -m new_name         # Rename branch
```

### Checkout
```bash
git checkout branch_name       # Switch branch
git checkout -b new-name       # Create + Switch to branch
```

### Rebase
⚠️ Warning: Don't rebase commits that have been pushed to shared repositories unless you coordinate with your team.
```bash
git rebase -i HEAD~3          # Interactive rebase (lets yoou edit last 3 commits)
```

---

##  Git Best Practices

### 1. Branch Strategy
- Always create a new branch 
  ```bash
  git checkout -b feature/your-feature-name
  ```
- 1 Feature = 1 Branch → Never commit directly to `main`

### 2. Sync Frequently
- Pull before you push (avoid conflicts)
  ```bash
  git pull origin main
  ```
- Small, frequent commits > big messy ones

### 3. Code Review
- Push → Create PR/MR (Pull/Merge Request)
- ✔️ Get approvals before merging to `main`

### 4. Clean History
- Write clear commit messages:
  ```bash
  git commit -m "Add user login validation"
  # Not "fixed stuff"
  ```
- Rebase instead of merge (keeps history clean)
  ```bash
  git pull --rebase origin main
  ```

### 5. Emergency Rules
- Never `--force` push to shared branches
- Test before merging to `main`
- Document special cases in Pull Request descriptions


