# Module 15: Git & GitHub Setup with SSH Access

**Learn Essential Version Control and SSH Authentication for Daily Development Work**

This practical module teaches you how to set up Git and GitHub with secure SSH authentication for everyday development tasks. You'll learn the fundamental skills needed to manage code, collaborate with others, and maintain project history using industry-standard tools and workflows.

**What You'll Learn:**
- Generate and configure SSH keys for secure GitHub access
- Set up Git with proper configuration for daily use
- Master basic Git workflows for individual and team projects
- Use .gitignore templates and file management
- Understand branching, merging, and collaboration basics
- Set up practical workflows for real-world development projects

## Learning Objectives

By completing this module, you will be able to:

1. **Set Up SSH Keys for GitHub**
   - Generate secure SSH key pairs using ED25519
   - Configure SSH keys for GitHub authentication
   - Test and troubleshoot SSH connections
   - Manage multiple SSH keys for different projects

2. **Configure Git for Daily Use**
   - Set up user identity and basic Git configuration
   - Understand Git workflows and common commands
   - Create and manage local repositories
   - Work with remote repositories and GitHub

3. **Master Basic Git Operations**
   - Stage, commit, and push changes effectively
   - Create and work with branches for features
   - Merge branches and resolve basic conflicts
   - Understand when to use merge vs rebase

4. **Use .gitignore and File Management**
   - Apply built-in .gitignore templates in VS Code and GitHub
   - Understand common patterns for ignoring files
   - Manage sensitive files and avoid accidental commits
   - Configure global ignore patterns

5. **Collaborate Using GitHub**
   - Fork repositories and create pull requests
   - Review code and provide feedback
   - Work with issues and project management
   - Understand basic team collaboration workflows

6. **Apply Practical Git Workflows**
   - Use feature branch workflow for development
   - Maintain clean commit history
   - Handle common Git problems and recovery
   - Set up efficient development environments
## Table of Contents

### [15.1 SSH Key Setup for GitHub](#151-ssh-key-setup-for-github)
- Generating SSH keys with ED25519
- Adding SSH keys to GitHub
- Testing SSH connections
- Managing multiple SSH keys

### [15.2 Git Installation and Basic Configuration](#152-git-installation-and-basic-configuration)
- Installing Git on Linux systems
- Setting up user identity and preferences
- Understanding Git configuration levels
- Creating useful Git aliases

### [15.3 Basic Git Operations and Workflow](#153-basic-git-operations-and-workflow)
- Repository initialization and cloning
- Staging, committing, and pushing changes
- Working with branches and merging
- Understanding Git history and logs

### [15.4 GitHub Integration and Collaboration](#154-github-integration-and-collaboration)
- Creating and managing repositories on GitHub
- Forking repositories and pull requests
- Working with issues and basic project management
- Team collaboration workflows

### [15.5 File Management with .gitignore](#155-file-management-with-gitignore)
- Using built-in .gitignore templates
- Common ignore patterns for different languages
- Global .gitignore configuration
- Managing sensitive files securely

### [15.6 Practical Git Workflows](#156-practical-git-workflows)
- Feature branch workflow
- Working with remote repositories
- Handling merge conflicts
- Git troubleshooting and recovery

## 15.1 SSH Key Setup for GitHub

### Understanding SSH Keys
SSH (Secure Shell) keys provide a secure way to authenticate with GitHub without entering your username and password every time. They use public-key cryptography where you have a key pair:
- **Private key**: Stays on your computer (never share this)
- **Public key**: Added to GitHub (safe to share)

### Generating SSH Keys
The modern standard is ED25519, which provides excellent security with smaller key sizes.

```bash
# Generate a new SSH key pair
ssh-keygen -t ed25519 -C "your_email@example.com"

# When prompted, you can:
# - Press Enter to use default file location (~/.ssh/id_ed25519)
# - Enter a secure passphrase (recommended)
```

### Adding SSH Key to SSH Agent
The SSH agent manages your keys and remembers your passphrase:

```bash
# Start the SSH agent
eval "$(ssh-agent -s)"

# Add your SSH key to the agent
ssh-add ~/.ssh/id_ed25519
```

### Adding SSH Key to GitHub
1. Copy your public key:
   ```bash
   cat ~/.ssh/id_ed25519.pub
   ```

2. Go to GitHub.com → Settings → SSH and GPG keys
3. Click "New SSH key"
4. Paste your public key and give it a title
5. Click "Add SSH key"

### Testing SSH Connection
```bash
# Test your SSH connection to GitHub
ssh -T git@github.com

# You should see: "Hi username! You've successfully authenticated..."
```

### SSH Configuration for Multiple Accounts
Create `~/.ssh/config` for managing multiple GitHub accounts:

```
# Personal GitHub account
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519

# Work GitHub account  
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/id_ed25519_work
```

## 15.2 Git Installation and Basic Configuration

### Installing Git
```bash
# Ubuntu/Debian
sudo apt update && sudo apt install git

# CentOS/RHEL/Rocky
sudo dnf install git

# Verify installation
git --version
```

### Basic Git Configuration
Set up your identity (this appears in commits):

```bash
# Set your name and email globally
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"

# Set default branch name
git config --global init.defaultBranch main

# Set preferred editor
git config --global core.editor nano  # or vim, code, etc.

# View your configuration
git config --list
```

### Useful Git Aliases
Make common commands shorter:

```bash
# Shorthand for common commands
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit

# Useful log formatting
git config --global alias.lg "log --oneline --graph --decorate"
```

### Git Configuration Levels
- **System**: Applies to all users (`/etc/gitconfig`)
- **Global**: Applies to your user (`~/.gitconfig`) 
- **Local**: Applies to specific repository (`.git/config`)

## 15.3 Basic Git Operations and Workflow

### Repository Operations
```bash
# Create a new repository
git init my-project
cd my-project

# Clone an existing repository
git clone git@github.com:username/repository.git
cd repository

# Check repository status
git status
```

### Basic Workflow
```bash
# 1. Check what has changed
git status
git diff

# 2. Stage files for commit
git add filename.txt        # Stage specific file
git add .                   # Stage all changes
git add -A                  # Stage all including deletions

# 3. Commit changes
git commit -m "Add new feature"

# 4. Push to GitHub
git push origin main
```

### Working with Branches
```bash
# List branches
git branch                  # Local branches
git branch -a              # All branches (local + remote)

# Create and switch to new branch
git checkout -b feature-name

# Switch between branches
git checkout main
git checkout feature-name

# Merge branch into main
git checkout main
git merge feature-name

# Delete branch after merging
git branch -d feature-name
```

### Viewing History
```bash
# View commit history
git log                     # Full history
git log --oneline          # Compact view
git log --graph            # With branch visualization
git log -5                 # Last 5 commits

# View changes in a commit
git show commit-hash
git show HEAD              # Latest commit
```

## 15.4 GitHub Integration and Collaboration

### Creating Repositories on GitHub
1. Go to GitHub.com and click "New repository"
2. Choose repository name and settings
3. Initialize with README if starting fresh
4. Clone to your computer:
   ```bash
   git clone git@github.com:username/repository.git
   ```

### Connecting Existing Repository to GitHub
```bash
# Add GitHub as remote origin
git remote add origin git@github.com:username/repository.git

# Push existing code to GitHub
git push -u origin main

# Verify remote configuration
git remote -v
```

### Pull Requests Workflow
1. **Fork the repository** (if not yours) or create a branch
2. **Make changes** in your fork/branch
3. **Push changes** to your fork/branch
4. **Create pull request** on GitHub
5. **Review and discuss** changes
6. **Merge** when approved

### Working with Issues
- Create issues to track bugs, features, or tasks
- Reference issues in commits: `git commit -m "Fix login bug, closes #42"`
- Use issue templates for consistency
- Assign issues to team members

### Basic Team Workflow
```bash
# Start working on new feature
git checkout main
git pull origin main                    # Get latest changes
git checkout -b feature/new-login      # Create feature branch

# Work on feature, make commits
git add .
git commit -m "Add login form"

# Push feature branch
git push origin feature/new-login

# Create pull request on GitHub
# After approval, merge and clean up
git checkout main
git pull origin main                    # Get merged changes
git branch -d feature/new-login        # Delete local branch
```

## 15.5 File Management with .gitignore

### Using Built-in Templates
Instead of writing .gitignore from scratch, use templates:

**In VS Code:**
1. Create new file named `.gitignore`
2. VS Code will suggest templates based on your project
3. Select appropriate template (Python, Node.js, etc.)

**In GitHub:**
1. When creating repository, check "Add .gitignore"
2. Choose template for your language/framework

**Command Line with GitHub Templates:**
```bash
# Download template directly
curl -o .gitignore https://raw.githubusercontent.com/github/gitignore/main/Python.gitignore
```

### Common Ignore Patterns
```gitignore
# OS generated files
.DS_Store
Thumbs.db

# Editor files
.vscode/
.idea/
*.swp

# Environment variables
.env
.env.local

# Logs
*.log
logs/

# Dependencies (example for Node.js)
node_modules/

# Build outputs
dist/
build/
```

### Global .gitignore
Set up patterns to ignore across all repositories:

```bash
# Create global gitignore file
echo ".DS_Store
Thumbs.db
.vscode/
*.swp" > ~/.gitignore_global

# Configure Git to use it
git config --global core.excludesfile ~/.gitignore_global
```

### Managing Sensitive Files
```bash
# If you accidentally committed secrets
git rm --cached secrets.txt           # Remove from tracking
echo "secrets.txt" >> .gitignore      # Add to .gitignore
git commit -m "Remove secrets from tracking"

# For files already committed with secrets, you may need:
# git filter-branch or BFG Repo-Cleaner (advanced topics)
```

## 15.6 Practical Git Workflows

### Feature Branch Workflow
```bash
# 1. Start with updated main branch
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/user-profiles

# 3. Work on feature (multiple commits OK)
git add .
git commit -m "Add user profile model"
git add .
git commit -m "Add profile editing form"

# 4. Push feature branch
git push origin feature/user-profiles

# 5. Create pull request on GitHub
# 6. After review and merge, clean up
git checkout main
git pull origin main
git branch -d feature/user-profiles
```

### Handling Merge Conflicts
```bash
# When git merge shows conflicts
git status                    # See conflicted files

# Edit conflicted files, look for:
# <<<<<<< HEAD
# Your changes
# =======
# Other changes  
# >>>>>>> branch-name

# After resolving conflicts
git add conflicted-file.txt
git commit -m "Resolve merge conflict"
```

### Common Git Recovery
```bash
# Undo last commit (keep changes)
git reset HEAD~1

# Undo last commit (discard changes)
git reset --hard HEAD~1

# Discard changes to a file
git checkout -- filename.txt

# Discard all local changes
git reset --hard HEAD

# View what changed in last few commits
git log --oneline -5
git show HEAD~1               # Show changes in previous commit
```

### Keeping Fork Updated
```bash
# Add upstream remote (original repository)
git remote add upstream git@github.com:original-owner/repository.git

# Update your fork
git checkout main
git fetch upstream
git merge upstream/main
git push origin main
```

**[⬆️ Back to Top](#module-15-git--github-setup-with-ssh-access)** | **[📚 Main Index](README.md)**

## Essential Command Reference

### SSH Key Management

| Operation | Command | Description |
|-----------|---------|-------------|
| **Generate Key** | `ssh-keygen -t ed25519 -C "email@example.com"` | Create new SSH key pair |
| **Start SSH Agent** | `eval "$(ssh-agent -s)"` | Start SSH agent |
| **Add Key to Agent** | `ssh-add ~/.ssh/id_ed25519` | Add private key to agent |
| **Test Connection** | `ssh -T git@github.com` | Test GitHub SSH connection |
| **View Public Key** | `cat ~/.ssh/id_ed25519.pub` | Display public key |

### Git Configuration

| Operation | Command | Description |
|-----------|---------|-------------|
| **Set Name** | `git config --global user.name "Your Name"` | Set global username |
| **Set Email** | `git config --global user.email "email@example.com"` | Set global email |
| **View Config** | `git config --list` | Show all configuration |
| **Set Editor** | `git config --global core.editor nano` | Set default editor |
| **Create Alias** | `git config --global alias.st status` | Create command alias |

### Repository Operations

| Operation | Command | Description |
|-----------|---------|-------------|
| **Initialize** | `git init` | Create new repository |
| **Clone** | `git clone git@github.com:user/repo.git` | Clone repository |
| **Status** | `git status` | Check repository status |
| **Add Remote** | `git remote add origin git@github.com:user/repo.git` | Add remote repository |
| **View Remotes** | `git remote -v` | List remote repositories |
### File Operations

| Operation | Command | Description |
|-----------|---------|-------------|
| **Stage File** | `git add filename.txt` | Stage specific file |
| **Stage All** | `git add .` | Stage all changes |
| **Commit** | `git commit -m "message"` | Create commit |
| **Push** | `git push origin main` | Push to remote |
| **Pull** | `git pull origin main` | Pull from remote |

### Branch Operations

| Operation | Command | Description |
|-----------|---------|-------------|
| **List Branches** | `git branch` | Show local branches |
| **Create Branch** | `git checkout -b feature-name` | Create and switch to branch |
| **Switch Branch** | `git checkout branch-name` | Switch to existing branch |
| **Merge Branch** | `git merge feature-name` | Merge branch into current |
| **Delete Branch** | `git branch -d feature-name` | Delete local branch |

### History and Information

| Operation | Command | Description |
|-----------|---------|-------------|
| **View History** | `git log` | Show commit history |
| **Compact Log** | `git log --oneline` | Show condensed history |
| **Show Changes** | `git show HEAD` | Show latest commit details |
| **View Diff** | `git diff` | Show unstaged changes |
| **View Staged** | `git diff --cached` | Show staged changes |

## Practical Workflows

### Setting Up New Project
```bash
# 1. Create repository on GitHub first
# 2. Clone to local machine
git clone git@github.com:username/project.git
cd project

# 3. Create initial files
echo "# My Project" > README.md
git add README.md
git commit -m "Initial commit"
git push origin main
```

### Feature Development Workflow
```bash
# 1. Start from main branch
git checkout main
git pull origin main

# 2. Create feature branch
git checkout -b feature/new-feature

# 3. Make changes and commit
git add .
git commit -m "Add new feature"

# 4. Push feature branch
git push origin feature/new-feature

# 5. Create pull request on GitHub
# 6. After merge, clean up
git checkout main
git pull origin main
git branch -d feature/new-feature
```

### Daily Git Workflow
```bash
# Check status and see changes
git status
git diff

# Stage and commit changes
git add .
git commit -m "Descriptive commit message"

# Push to GitHub
git push origin main

# Pull latest changes from team
git pull origin main
```

## Troubleshooting Common Issues

### SSH Connection Problems
```bash
# Test SSH connection
ssh -T git@github.com

# If connection fails, check SSH agent
ssh-add -l

# Restart SSH agent if needed
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/id_ed25519
```

### Git Authentication Issues
```bash
# Switch from HTTPS to SSH
git remote set-url origin git@github.com:username/repository.git

# Verify remote URL
git remote -v
```

### Merge Conflicts
```bash
# When merge conflict occurs
git status  # Shows conflicted files

# Edit files to resolve conflicts
# Look for <<<<<<< HEAD, =======, >>>>>>> markers
# Remove markers and choose correct content

# After resolving
git add conflicted-file.txt
git commit -m "Resolve merge conflict"
```

### Undo Operations
```bash
# Undo last commit (keep changes)
git reset HEAD~1

# Undo changes to specific file
git checkout -- filename.txt

# Discard all local changes
git reset --hard HEAD
```

**[⬆️ Back to Top](#module-15-git--github-setup-with-ssh-access)** | **[📚 Main Index](README.md)**

## Lab Exercises

### Lab 1: SSH Key Setup and GitHub Authentication
**Objective:** Set up secure SSH authentication for GitHub access

**Duration:** 30 minutes

**Tasks:**
1. **Generate SSH Key Pair**
   - Create ED25519 SSH key with your email
   - Set a secure passphrase
   - Start SSH agent and add key

2. **Configure GitHub SSH Access**
   - Add public key to GitHub account
   - Test SSH connection to GitHub
   - Verify authentication is working

3. **SSH Configuration**
   - Create SSH config file for GitHub
   - Test connection using config
   - Document the setup process

**Verification:**
- SSH connection test shows successful authentication
- Can clone repositories using SSH URLs
- SSH agent properly manages the key

### Lab 2: Git Configuration and Repository Setup  
**Objective:** Configure Git and create your first repository

**Duration:** 45 minutes

**Tasks:**
1. **Git Configuration**
   - Set global username and email
   - Configure default editor and aliases
   - Set up global .gitignore file

2. **Repository Creation**
   - Create new repository on GitHub
   - Clone repository locally
   - Add README.md and initial commit

3. **Basic Git Workflow**
   - Make changes to README.md
   - Stage, commit, and push changes
   - Verify changes appear on GitHub

**Verification:**
- Git configuration properly set
- Repository successfully created and cloned
- Changes successfully pushed to GitHub

### Lab 3: Branch Workflow and Collaboration
**Objective:** Practice feature branch workflow and collaboration

**Duration:** 60 minutes

**Tasks:**
1. **Feature Branch Workflow**
   - Create feature branch for new functionality
   - Make multiple commits on feature branch
   - Push feature branch to GitHub

2. **Pull Request Process**
   - Create pull request for your feature
   - Add description and request review
   - Merge pull request when approved

3. **Repository Maintenance**
   - Delete merged feature branch
   - Update local main branch
   - Practice conflict resolution (simulate conflict)

**Verification:**
- Feature branch successfully created and pushed
- Pull request properly created and merged
- Local repository properly cleaned up after merge

### Lab 4: File Management with .gitignore
**Objective:** Master file management and ignore patterns

**Duration:** 30 minutes

**Tasks:**
1. **Using Built-in Templates**
   - Create new project with specific language focus
   - Apply appropriate .gitignore template
   - Test ignore patterns with sample files

2. **Custom Ignore Patterns**
   - Add custom patterns for your environment
   - Set up global .gitignore file
   - Test global ignore patterns

3. **Sensitive File Management**
   - Practice removing accidentally committed files
   - Set up environment file handling
   - Document security best practices

**Verification:**
- .gitignore templates properly applied
- Custom patterns working correctly
- Sensitive files properly excluded from version control

**[⬆️ Back to Top](#module-15-git--github-setup-with-ssh-access)** | **[📚 Main Index](README.md)**

---

## Summary

This module provided practical training in Git and GitHub fundamentals with SSH authentication. You've learned essential skills for:

- **SSH Key Management**: Secure authentication setup with ED25519 keys
- **Git Configuration**: Personal and global settings for efficient development
- **Repository Operations**: Cloning, committing, pushing, and collaboration workflows
- **Branch Management**: Feature branches and merge strategies for team development
- **File Management**: Using .gitignore templates and handling sensitive files
- **Troubleshooting**: Common Git and SSH issues and their solutions

### Key Takeaways

1. **Security First**: Always use SSH keys with passphrases for GitHub authentication
2. **Consistent Workflow**: Establish predictable patterns for daily Git operations
3. **Template Usage**: Leverage built-in .gitignore templates rather than creating custom ones
4. **Branch Strategy**: Use feature branches to keep main branch stable
5. **Clear Commits**: Write descriptive commit messages that explain the "why"

### Next Steps

- Practice the workflows daily to build muscle memory
- Explore GitHub features like Issues, Projects, and Actions
- Learn about Git hooks for automation
- Consider advanced topics like rebasing and cherry-picking when needed
- Set up automated backups and sync for important repositories

**You're now ready to use Git and GitHub effectively for version control and collaboration!**

**[⬆️ Back to Top](#module-15-git--github-setup-with-ssh-access)** | **[📚 Main Index](README.md)**
