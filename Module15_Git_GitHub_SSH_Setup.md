# Module 15: Git & GitHub Setup with SSH Access

## Overview
This module walks through setting up a GitHub repository, configuring SSH access for secure authentication, and using Git effectively for version control. It also covers `.git/config` internals and best practices for `.gitignore`. Engineers will learn to establish secure, passwordless authentication with GitHub and implement professional Git workflows for infrastructure code management.

**Key Points:**
- Generate SSH keys and configure GitHub for passwordless access
- Clone, push, pull, and manage repositories using Git CLI
- Understand `.git/config` structure and override behavior
- Create effective `.gitignore` files to avoid committing sensitive or unnecessary files
- Use Git branches, commits, and remotes with confidence

## Learning Objectives
By the end of this module, you will be able to:
1. Generate and register SSH keys with GitHub for secure Git operations
2. Create and clone repositories using SSH URLs
3. Perform Git operations: `add`, `commit`, `push`, `pull`, `status`, `log`, and `branch`
4. Inspect and modify `.git/config` to manage remotes, aliases, and user settings
5. Write `.gitignore` rules to exclude build artifacts, secrets, and system files
6. Follow Git best practices for commit messages, branching, and collaboration

## Topics

### 15.1 SSH Key Generation and GitHub Integration
- ED25519 vs RSA key selection for GitHub
- SSH key generation with proper security parameters
- GitHub SSH key registration and verification
- SSH agent configuration and key management
- Troubleshooting SSH authentication issues

### 15.2 Git Repository Setup and Clone Operations
- Repository initialization and structure
- SSH vs HTTPS URL comparison and selection
- Clone operations with different authentication methods
- Remote repository configuration and management
- Multiple remote handling (origin, upstream, etc.)

### 15.3 Essential Git Operations and Workflow
- Staging area concepts and file lifecycle
- Commit creation with meaningful messages
- Push and pull operations with conflict resolution
- Branch creation, switching, and management
- Status checking and history navigation

### 15.4 Git Configuration Management
- Understanding `.git/config` structure and hierarchy
- Global vs local configuration precedence
- User identity and authentication settings
- Alias creation for common operations
- Advanced configuration options and hooks

### 15.5 Advanced .gitignore Patterns and Best Practices
- Pattern syntax and wildcard usage
- Language-specific and framework-specific ignores
- Security considerations for sensitive files
- Global vs project-specific ignore files
- Dynamic ignore patterns and exceptions

### 15.6 Professional Git Workflow and Collaboration
- Branching strategies (feature, release, hotfix)
- Commit message conventions and standards
- Code review workflows and pull requests
- Merge vs rebase strategies
- Collaborative development best practices

## Practical Examples

### SSH Key Generation and GitHub Setup

#### Generate Secure SSH Keys for GitHub
```bash
# Generate ED25519 key (recommended for GitHub)
ssh-keygen -t ed25519 -C "your_email@example.com" -f ~/.ssh/github_ed25519

# Alternative: Generate RSA key (legacy compatibility)
ssh-keygen -t rsa -b 4096 -C "your_email@example.com" -f ~/.ssh/github_rsa

# Set proper permissions
chmod 600 ~/.ssh/github_ed25519
chmod 644 ~/.ssh/github_ed25519.pub

# Start SSH agent and add key
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_ed25519

# Display public key for GitHub registration
echo "Copy this public key to GitHub:"
cat ~/.ssh/github_ed25519.pub
```

#### Configure SSH for GitHub Access
```bash
# Create/edit SSH config for GitHub
# ~/.ssh/config
Host github.com
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_ed25519
    IdentitiesOnly yes
    AddKeysToAgent yes
    UseKeychain yes  # macOS only

# Alternative host configuration for multiple GitHub accounts
Host github-work
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_work_ed25519
    IdentitiesOnly yes

Host github-personal
    HostName github.com
    User git
    IdentityFile ~/.ssh/github_personal_ed25519
    IdentitiesOnly yes

# Test SSH connection to GitHub
ssh -T git@github.com

# Expected output:
# Hi username! You've successfully authenticated, but GitHub does not provide shell access.
```

#### SSH Key Management Script
```bash
#!/bin/bash
# github-ssh-setup.sh - Automated GitHub SSH setup

EMAIL="$1"
KEY_NAME="${2:-github_ed25519}"
KEY_TYPE="${3:-ed25519}"

if [[ -z "$EMAIL" ]]; then
    echo "Usage: $0 <email> [key_name] [key_type]"
    echo "Example: $0 user@example.com github_ed25519 ed25519"
    exit 1
fi

SSH_DIR="$HOME/.ssh"
KEY_FILE="$SSH_DIR/$KEY_NAME"

# Create SSH directory if it doesn't exist
mkdir -p "$SSH_DIR"
chmod 700 "$SSH_DIR"

# Generate SSH key
echo "Generating $KEY_TYPE SSH key for GitHub..."
ssh-keygen -t "$KEY_TYPE" -C "$EMAIL" -f "$KEY_FILE" -N ""

# Set proper permissions
chmod 600 "$KEY_FILE"
chmod 644 "$KEY_FILE.pub"

# Add to SSH agent
eval "$(ssh-agent -s)"
ssh-add "$KEY_FILE"

# Update SSH config
SSH_CONFIG="$SSH_DIR/config"
if ! grep -q "Host github.com" "$SSH_CONFIG" 2>/dev/null; then
    cat >> "$SSH_CONFIG" << EOF

# GitHub configuration
Host github.com
    HostName github.com
    User git
    IdentityFile $KEY_FILE
    IdentitiesOnly yes
    AddKeysToAgent yes
EOF
    echo "Added GitHub configuration to SSH config"
fi

echo "Public key (copy this to GitHub):"
echo "========================================="
cat "$KEY_FILE.pub"
echo "========================================="
echo ""
echo "Next steps:"
echo "1. Copy the public key above"
echo "2. Go to GitHub → Settings → SSH and GPG keys"
echo "3. Click 'New SSH key'"
echo "4. Paste the public key and save"
echo "5. Test with: ssh -T git@github.com"
```

### Git Repository Operations

#### Repository Initialization and Setup
```bash
# Initialize a new Git repository
git init project-name
cd project-name

# Configure user identity (local to this repo)
git config user.name "Your Name"
git config user.email "your.email@example.com"

# Create initial file and commit
echo "# Project Name" > README.md
git add README.md
git commit -m "Initial commit: Add README"

# Add remote repository (SSH URL)
git remote add origin git@github.com:username/project-name.git

# Push to GitHub
git push -u origin main

# Verify remote configuration
git remote -v
git remote show origin
```

#### Clone Operations and Remote Management
```bash
# Clone repository using SSH
git clone git@github.com:username/repository.git
cd repository

# Clone with custom directory name
git clone git@github.com:username/repository.git my-project

# Clone specific branch
git clone -b develop git@github.com:username/repository.git

# Clone with limited history (shallow clone)
git clone --depth 1 git@github.com:username/repository.git

# Add upstream remote for forked repositories
git remote add upstream git@github.com:original-owner/repository.git

# Fetch from all remotes
git fetch --all

# Set up tracking for upstream branch
git branch --set-upstream-to=upstream/main main
```

#### Essential Git Workflow Operations
```bash
# Check repository status
git status
git status --short  # Concise output

# View commit history
git log --oneline --graph --decorate
git log --author="username" --since="2 weeks ago"
git log --grep="feature" --oneline

# Stage files for commit
git add file1.txt file2.txt    # Stage specific files
git add .                      # Stage all changes
git add -A                     # Stage all changes including deletions
git add -p                     # Interactive staging

# Create commits
git commit -m "Add user authentication module"
git commit -am "Fix: Resolve login timeout issue"  # Stage and commit modified files

# Push changes
git push origin main
git push origin feature-branch
git push --force-with-lease origin feature-branch  # Safer force push

# Pull changes
git pull origin main
git pull --rebase origin main  # Rebase instead of merge

# Branch operations
git branch                     # List local branches
git branch -a                  # List all branches (local and remote)
git branch feature/new-module  # Create new branch
git checkout feature/new-module # Switch to branch
git checkout -b feature/auth   # Create and switch to new branch
git branch -d feature/old      # Delete merged branch
git branch -D feature/old      # Force delete branch

# Merge operations
git checkout main
git merge feature/auth
git merge --no-ff feature/auth  # Force merge commit
```

### Git Configuration Deep Dive

#### Understanding .git/config Structure
```bash
# View repository configuration
cat .git/config

# Example .git/config content:
[core]
    repositoryformatversion = 0
    filemode = true
    bare = false
    logallrefupdates = true
    ignorecase = true
    precomposeunicode = true

[remote "origin"]
    url = git@github.com:username/project.git
    fetch = +refs/heads/*:refs/remotes/origin/*

[remote "upstream"]
    url = git@github.com:original-owner/project.git
    fetch = +refs/heads/*:refs/remotes/upstream/*

[branch "main"]
    remote = origin
    merge = refs/heads/main

[branch "develop"]
    remote = origin
    merge = refs/heads/develop

[user]
    name = Your Name
    email = your.email@example.com

[alias]
    st = status
    co = checkout
    br = branch
    ci = commit
    lg = log --oneline --graph --decorate
    unstage = reset HEAD --
```

#### Git Configuration Management
```bash
# View all configuration settings
git config --list
git config --list --show-origin  # Show where each setting comes from

# Global configuration (applies to all repositories)
git config --global user.name "Your Name"
git config --global user.email "your.email@example.com"
git config --global init.defaultBranch main
git config --global core.editor vim

# Local configuration (repository-specific)
git config user.name "Work Name"
git config user.email "work.email@company.com"

# Useful global aliases
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.unstage 'reset HEAD --'
git config --global alias.last 'log -1 HEAD'
git config --global alias.visual '!gitk'

# Advanced aliases for logging
git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
git config --global alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit"
git config --global alias.lola "log --graph --decorate --pretty=oneline --abbrev-commit --all"

# Security and performance settings
git config --global credential.helper cache
git config --global credential.helper 'cache --timeout=3600'
git config --global core.autocrlf input  # Linux/macOS
git config --global core.safecrlf true
git config --global push.default simple
git config --global pull.rebase false

# View specific configuration
git config user.name
git config --get remote.origin.url
```

#### Advanced Git Configuration Script
```bash
#!/bin/bash
# git-setup.sh - Comprehensive Git configuration

setup_global_config() {
    local name="$1"
    local email="$2"
    
    echo "Setting up global Git configuration..."
    
    # User identity
    git config --global user.name "$name"
    git config --global user.email "$email"
    
    # Default branch
    git config --global init.defaultBranch main
    
    # Editor and diff tool
    git config --global core.editor vim
    git config --global merge.tool vimdiff
    
    # Line ending handling
    git config --global core.autocrlf input
    git config --global core.safecrlf true
    
    # Push and pull behavior
    git config --global push.default simple
    git config --global pull.rebase false
    
    # Performance settings
    git config --global core.preloadindex true
    git config --global core.fscache true
    git config --global gc.auto 256
    
    echo "Global configuration completed"
}

setup_aliases() {
    echo "Setting up useful Git aliases..."
    
    # Basic aliases
    git config --global alias.st status
    git config --global alias.co checkout
    git config --global alias.br branch
    git config --global alias.ci commit
    git config --global alias.cp cherry-pick
    
    # Advanced aliases
    git config --global alias.unstage 'reset HEAD --'
    git config --global alias.last 'log -1 HEAD'
    git config --global alias.uncommit 'reset --soft HEAD~1'
    git config --global alias.amend 'commit --amend'
    
    # Logging aliases
    git config --global alias.lg "log --color --graph --pretty=format:'%Cred%h%Creset -%C(yellow)%d%Creset %s %Cgreen(%cr) %C(bold blue)<%an>%Creset' --abbrev-commit"
    git config --global alias.lol "log --graph --decorate --pretty=oneline --abbrev-commit"
    git config --global alias.lola "log --graph --decorate --pretty=oneline --abbrev-commit --all"
    git config --global alias.tree "log --graph --full-history --all --color --pretty=format:'%x1b[31m%h%x09%x1b[32m%d%x1b[0m%x20%s'"
    
    # Status and diff aliases
    git config --global alias.s "status --short --branch"
    git config --global alias.d "diff"
    git config --global alias.dc "diff --cached"
    git config --global alias.ds "diff --stat"
    
    echo "Aliases configured successfully"
}

setup_gitignore_global() {
    local gitignore_global="$HOME/.gitignore_global"
    
    echo "Setting up global .gitignore..."
    
    cat > "$gitignore_global" << 'EOF'
# Global .gitignore for all repositories

# OS generated files
.DS_Store
.DS_Store?
._*
.Spotlight-V100
.Trashes
ehthumbs.db
Thumbs.db
*~

# Editor and IDE files
.vscode/
.idea/
*.swp
*.swo
*~
.sublime-project
.sublime-workspace

# Logs
*.log
npm-debug.log*
yarn-debug.log*
yarn-error.log*

# Runtime data
pids
*.pid
*.seed
*.pid.lock

# Temporary files
*.tmp
*.temp
.cache/

# Archives
*.7z
*.dmg
*.gz
*.iso
*.jar
*.rar
*.tar
*.zip

# Security sensitive files
.env
.env.local
.env.*.local
*.pem
*.key
*.crt
id_rsa
id_dsa
id_ecdsa
id_ed25519
EOF

    # Configure Git to use global gitignore
    git config --global core.excludesfile "$gitignore_global"
    
    echo "Global .gitignore configured at: $gitignore_global"
}

# Main setup function
main() {
    local name="$1"
    local email="$2"
    
    if [[ -z "$name" || -z "$email" ]]; then
        echo "Usage: $0 \"Your Name\" \"your.email@example.com\""
        exit 1
    fi
    
    setup_global_config "$name" "$email"
    setup_aliases
    setup_gitignore_global
    
    echo ""
    echo "Git configuration completed successfully!"
    echo "Review your configuration with: git config --list --global"
}

main "$@"
```

### Advanced .gitignore Patterns and Management

#### Comprehensive .gitignore Examples
```bash
# .gitignore - Comprehensive patterns for infrastructure projects

# ===================================
# OPERATING SYSTEM FILES
# ===================================

# macOS
.DS_Store
.AppleDouble
.LSOverride
._*
.Spotlight-V100
.Trashes

# Windows
Thumbs.db
ehthumbs.db
Desktop.ini
$RECYCLE.BIN/
*.lnk

# Linux
*~
.nfs*

# ===================================
# EDITOR AND IDE FILES
# ===================================

# Visual Studio Code
.vscode/
*.code-workspace

# IntelliJ IDEA
.idea/
*.iml
*.ipr
*.iws

# Vim
*.swp
*.swo
*~
.vimrc.local

# Emacs
*~
\#*\#
/.emacs.desktop
/.emacs.desktop.lock
*.elc
auto-save-list
tramp
.\#*

# Sublime Text
*.sublime-project
*.sublime-workspace

# ===================================
# PROGRAMMING LANGUAGES
# ===================================

# Python
__pycache__/
*.py[cod]
*$py.class
*.so
.Python
build/
develop-eggs/
dist/
downloads/
eggs/
.eggs/
lib/
lib64/
parts/
sdist/
var/
wheels/
*.egg-info/
.installed.cfg
*.egg
MANIFEST
.env
.venv
env/
venv/
ENV/
env.bak/
venv.bak/
.pytest_cache/
.coverage
.tox/

# Node.js
node_modules/
npm-debug.log*
yarn-debug.log*
yarn-error.log*
.npm
.eslintcache
.node_repl_history
*.tgz
.yarn-integrity
.env.local
.env.development.local
.env.test.local
.env.production.local

# Java
*.class
*.jar
*.war
*.ear
*.nar
hs_err_pid*
target/
.gradle/
build/
.classpath
.project
.settings/

# Go
*.exe
*.exe~
*.dll
*.so
*.dylib
*.test
*.out
vendor/
*.sum

# ===================================
# DEVOPS AND INFRASTRUCTURE
# ===================================

# Terraform
*.tfstate
*.tfstate.*
.terraform/
.terraform.lock.hcl
*.tfvars
!example.tfvars
*.auto.tfvars
crash.log
*.tfplan
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Ansible
*.retry
.vault_pass
host_vars/
group_vars/
ansible.cfg.local

# Docker
.docker/
docker-compose.override.yml
.dockerignore

# Kubernetes
*.kubeconfig
*-kubeconfig
kubeconfig
.kube/config

# Vagrant
.vagrant/
*.box

# ===================================
# CLOUD PROVIDERS
# ===================================

# AWS
.aws/
*.pem

# Azure
.azure/

# Google Cloud
.gcloud/
*.json  # Service account keys

# ===================================
# SECRETS AND CREDENTIALS
# ===================================

# Environment files
.env
.env.*
!.env.example
!.env.template

# SSH keys
id_rsa
id_dsa
id_ecdsa
id_ed25519
*.pem
*.key
*.crt
*.p12
*.pfx

# Configuration files with secrets
config.local.*
*-config.local.*
secrets.yaml
secrets.yml
*-secrets.*

# Database dumps
*.sql
*.dump
*.db

# ===================================
# LOGS AND TEMPORARY FILES
# ===================================

# Logs
*.log
logs/
log/
*.out

# Temporary files
*.tmp
*.temp
.cache/
.tmp/
tmp/

# Backup files
*.bak
*.backup
*~

# ===================================
# BUILD ARTIFACTS
# ===================================

# General build outputs
dist/
build/
out/
target/
bin/
obj/

# Archives
*.zip
*.tar.gz
*.rar
*.7z

# Compiled objects
*.o
*.lo
*.slo
*.ko
*.obj
*.elf
*.exe
*.dll
*.so
*.dylib
```

#### .gitignore Management Tools
```bash
#!/bin/bash
# gitignore-manager.sh - Manage .gitignore files effectively

GITIGNORE_TEMPLATES_DIR="$HOME/.gitignore-templates"
GITIGNORE_API="https://www.toptal.com/developers/gitignore/api"

# Create directory for templates
mkdir -p "$GITIGNORE_TEMPLATES_DIR"

generate_gitignore() {
    local technologies="$1"
    local output_file="${2:-.gitignore}"
    
    echo "Generating .gitignore for: $technologies"
    
    # Download from gitignore.io API
    curl -L -s "$GITIGNORE_API/$technologies" > "$output_file"
    
    if [[ $? -eq 0 ]]; then
        echo "Generated $output_file successfully"
        echo "Preview:"
        head -20 "$output_file"
    else
        echo "Failed to generate .gitignore"
        return 1
    fi
}

list_available_templates() {
    echo "Available .gitignore templates:"
    curl -L -s "$GITIGNORE_API/list" | tr ',' '\n' | sort
}

create_custom_gitignore() {
    local project_type="$1"
    local gitignore_file=".gitignore"
    
    case "$project_type" in
        "terraform")
            cat > "$gitignore_file" << 'EOF'
# Terraform files
*.tfstate
*.tfstate.*
.terraform/
.terraform.lock.hcl
*.tfvars
!example.tfvars
*.auto.tfvars
crash.log
*.tfplan
override.tf
override.tf.json
*_override.tf
*_override.tf.json

# Ansible files
*.retry
.vault_pass

# SSH keys and certificates
*.pem
*.key
*.crt
id_rsa*
id_ecdsa*
id_ed25519*

# Environment files
.env
.env.*
!.env.example

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db
EOF
            ;;
        "ansible")
            cat > "$gitignore_file" << 'EOF'
# Ansible files
*.retry
.vault_pass
host_vars/*/vault.yml
group_vars/*/vault.yml
ansible.cfg.local

# SSH keys
*.pem
*.key
id_rsa*
id_ecdsa*
id_ed25519*

# Environment files
.env
inventory.local
hosts.local

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
EOF
            ;;
        "docker")
            cat > "$gitignore_file" << 'EOF'
# Docker files
.dockerignore.local
docker-compose.override.yml
docker-compose.override.yaml
.docker/

# Environment files
.env
.env.*
!.env.example

# Build artifacts
dist/
build/

# IDE files
.vscode/
.idea/
*.swp

# OS files
.DS_Store
Thumbs.db

# Logs
*.log
logs/
EOF
            ;;
        *)
            echo "Unknown project type: $project_type"
            echo "Available types: terraform, ansible, docker"
            return 1
            ;;
    esac
    
    echo "Created custom .gitignore for $project_type"
}

check_gitignore_coverage() {
    local directory="${1:-.}"
    
    echo "Checking .gitignore coverage in: $directory"
    
    # Find files that might need to be ignored
    find "$directory" -type f \( \
        -name "*.log" -o \
        -name "*.tmp" -o \
        -name "*.temp" -o \
        -name "*.bak" -o \
        -name "*.backup" -o \
        -name ".DS_Store" -o \
        -name "Thumbs.db" -o \
        -name "*.swp" -o \
        -name "*.swo" -o \
        -name ".env" -o \
        -name "*.tfstate" -o \
        -name "*.tfvars" -o \
        -name "*.pem" -o \
        -name "*.key" \
        \) -not -path "./.git/*" | head -20
    
    echo ""
    echo "Consider adding these patterns to .gitignore if they shouldn't be tracked"
}

# Usage examples
case "${1:-help}" in
    "generate")
        generate_gitignore "$2" "$3"
        ;;
    "list")
        list_available_templates
        ;;
    "custom")
        create_custom_gitignore "$2"
        ;;
    "check")
        check_gitignore_coverage "$2"
        ;;
    "help")
        echo "Usage: $0 {generate|list|custom|check} [args...]"
        echo ""
        echo "Commands:"
        echo "  generate <technologies> [output_file]  - Generate .gitignore from gitignore.io"
        echo "  list                                   - List available templates"
        echo "  custom <project_type>                  - Create custom .gitignore"
        echo "  check [directory]                      - Check for files that might need ignoring"
        echo ""
        echo "Examples:"
        echo "  $0 generate linux,macos,windows,python"
        echo "  $0 custom terraform"
        echo "  $0 check /path/to/project"
        ;;
esac
```

### Professional Git Workflow and Best Practices

#### Git Branching Strategies
```bash
# Feature Branch Workflow
git checkout main
git pull origin main
git checkout -b feature/user-authentication
# ... work on feature ...
git add .
git commit -m "feat: Add user authentication system"
git push origin feature/user-authentication
# Create pull request, get review, merge

# Git Flow Workflow
# Initialize git flow
git flow init

# Start new feature
git flow feature start new-feature
# ... work on feature ...
git add .
git commit -m "Add new feature implementation"
git flow feature finish new-feature

# Start release
git flow release start 1.2.0
# ... prepare release ...
git flow release finish 1.2.0

# Hotfix
git flow hotfix start emergency-fix
# ... fix critical issue ...
git flow hotfix finish emergency-fix

# GitHub Flow (simplified)
git checkout main
git pull origin main
git checkout -b fix/security-vulnerability
# ... fix issue ...
git commit -m "fix: Patch security vulnerability in auth module"
git push origin fix/security-vulnerability
# Create pull request, review, merge, delete branch
```

#### Commit Message Best Practices
```bash
# Conventional Commit Format
# <type>[optional scope]: <description>
# 
# [optional body]
# 
# [optional footer(s)]

# Examples of good commit messages:
git commit -m "feat: Add SSH key rotation functionality"
git commit -m "fix: Resolve memory leak in connection pooling"
git commit -m "docs: Update SSH configuration guide"
git commit -m "refactor: Simplify user authentication logic"
git commit -m "test: Add unit tests for SSH key validation"
git commit -m "chore: Update dependencies to latest versions"

# Multi-line commit with body and footer
git commit -m "feat: Implement automated backup system

Add scheduled backup functionality with configurable retention policies.
Supports both local and remote storage backends.

Closes #123
Reviewed-by: @senior-engineer"

# Breaking changes
git commit -m "feat!: Change SSH key format to ED25519 only

BREAKING CHANGE: RSA keys are no longer supported. All existing RSA keys
must be migrated to ED25519 format before upgrading."
```

#### Advanced Git Operations Script
```bash
#!/bin/bash
# git-workflow-tools.sh - Advanced Git workflow automation

# Colors for output
RED='\033[0;31m'
GREEN='\033[0;32m'
YELLOW='\033[1;33m'
BLUE='\033[0;34m'
NC='\033[0m' # No Color

log_info() { echo -e "${BLUE}INFO:${NC} $1"; }
log_success() { echo -e "${GREEN}SUCCESS:${NC} $1"; }
log_warning() { echo -e "${YELLOW}WARNING:${NC} $1"; }
log_error() { echo -e "${RED}ERROR:${NC} $1"; }

create_feature_branch() {
    local feature_name="$1"
    local base_branch="${2:-main}"
    
    if [[ -z "$feature_name" ]]; then
        log_error "Feature name is required"
        return 1
    fi
    
    log_info "Creating feature branch: feature/$feature_name"
    
    # Ensure we're on the base branch
    git checkout "$base_branch"
    git pull origin "$base_branch"
    
    # Create and checkout feature branch
    git checkout -b "feature/$feature_name"
    
    log_success "Feature branch created: feature/$feature_name"
}

finish_feature() {
    local current_branch=$(git branch --show-current)
    local main_branch="${1:-main}"
    
    if [[ ! "$current_branch" =~ ^feature/ ]]; then
        log_error "Not on a feature branch"
        return 1
    fi
    
    log_info "Finishing feature branch: $current_branch"
    
    # Push feature branch
    git push origin "$current_branch"
    
    # Switch to main and update
    git checkout "$main_branch"
    git pull origin "$main_branch"
    
    # Merge feature branch
    git merge --no-ff "$current_branch"
    
    # Push merged changes
    git push origin "$main_branch"
    
    # Delete feature branch
    git branch -d "$current_branch"
    git push origin --delete "$current_branch"
    
    log_success "Feature branch merged and cleaned up"
}

create_release() {
    local version="$1"
    local main_branch="${2:-main}"
    
    if [[ -z "$version" ]]; then
        log_error "Version is required (e.g., 1.2.0)"
        return 1
    fi
    
    log_info "Creating release: $version"
    
    # Ensure we're on main and up to date
    git checkout "$main_branch"
    git pull origin "$main_branch"
    
    # Create release branch
    git checkout -b "release/$version"
    
    # Update version files if they exist
    if [[ -f "VERSION" ]]; then
        echo "$version" > VERSION
        git add VERSION
        git commit -m "chore: Bump version to $version"
    fi
    
    log_success "Release branch created: release/$version"
    log_info "Make final adjustments, then run: git-workflow-tools.sh finish_release $version"
}

finish_release() {
    local version="$1"
    local main_branch="${2:-main}"
    local develop_branch="${3:-develop}"
    
    if [[ -z "$version" ]]; then
        log_error "Version is required"
        return 1
    fi
    
    local release_branch="release/$version"
    local current_branch=$(git branch --show-current)
    
    if [[ "$current_branch" != "$release_branch" ]]; then
        log_error "Not on release branch: $release_branch"
        return 1
    fi
    
    log_info "Finishing release: $version"
    
    # Merge to main
    git checkout "$main_branch"
    git pull origin "$main_branch"
    git merge --no-ff "$release_branch"
    
    # Create tag
    git tag -a "v$version" -m "Release version $version"
    
    # Push main and tags
    git push origin "$main_branch"
    git push origin "v$version"
    
    # Merge to develop if it exists
    if git show-ref --verify --quiet "refs/heads/$develop_branch"; then
        git checkout "$develop_branch"
        git pull origin "$develop_branch"
        git merge --no-ff "$release_branch"
        git push origin "$develop_branch"
    fi
    
    # Clean up release branch
    git branch -d "$release_branch"
    git push origin --delete "$release_branch"
    
    log_success "Release $version completed and tagged"
}

create_hotfix() {
    local hotfix_name="$1"
    local main_branch="${2:-main}"
    
    if [[ -z "$hotfix_name" ]]; then
        log_error "Hotfix name is required"
        return 1
    fi
    
    log_info "Creating hotfix branch: hotfix/$hotfix_name"
    
    # Create hotfix from main
    git checkout "$main_branch"
    git pull origin "$main_branch"
    git checkout -b "hotfix/$hotfix_name"
    
    log_success "Hotfix branch created: hotfix/$hotfix_name"
}

sync_fork() {
    local upstream_remote="${1:-upstream}"
    local main_branch="${2:-main}"
    
    log_info "Syncing fork with upstream"
    
    # Fetch upstream
    git fetch "$upstream_remote"
    
    # Checkout main and merge upstream
    git checkout "$main_branch"
    git merge "$upstream_remote/$main_branch"
    
    # Push to origin
    git push origin "$main_branch"
    
    log_success "Fork synced with upstream"
}

clean_branches() {
    log_info "Cleaning up merged branches"
    
    # Delete local branches that have been merged
    git branch --merged main | grep -v "main\|develop" | xargs -n 1 git branch -d
    
    # Prune remote branches
    git remote prune origin
    
    log_success "Branch cleanup completed"
}

# Main function
main() {
    local command="$1"
    shift
    
    case "$command" in
        "feature")
            create_feature_branch "$@"
            ;;
        "finish-feature")
            finish_feature "$@"
            ;;
        "release")
            create_release "$@"
            ;;
        "finish-release")
            finish_release "$@"
            ;;
        "hotfix")
            create_hotfix "$@"
            ;;
        "sync-fork")
            sync_fork "$@"
            ;;
        "clean")
            clean_branches "$@"
            ;;
        *)
            echo "Git Workflow Tools"
            echo "=================="
            echo ""
            echo "Usage: $0 <command> [args...]"
            echo ""
            echo "Commands:"
            echo "  feature <name> [base]        - Create feature branch"
            echo "  finish-feature [main]        - Finish current feature branch"
            echo "  release <version> [main]     - Create release branch"
            echo "  finish-release <version>     - Finish release branch"
            echo "  hotfix <name> [main]         - Create hotfix branch"
            echo "  sync-fork [upstream] [main]  - Sync fork with upstream"
            echo "  clean                        - Clean up merged branches"
            echo ""
            echo "Examples:"
            echo "  $0 feature user-auth"
            echo "  $0 release 1.2.0"
            echo "  $0 hotfix security-patch"
            exit 1
            ;;
    esac
}

main "$@"
```

## Git Security and Best Practices

| Category | Best Practice | Implementation |
|----------|---------------|----------------|
| Authentication | Use SSH keys with passphrase | ED25519 keys with SSH agent |
| Commit Signing | Sign commits with GPG | `git config --global commit.gpgsign true` |
| Sensitive Data | Never commit secrets | Use .gitignore and git-secrets tool |
| Branch Protection | Protect main branch | GitHub branch protection rules |
| Code Review | Require pull request reviews | GitHub/GitLab review workflows |
| Access Control | Use fine-grained permissions | Repository and organization settings |
| Audit Trail | Enable audit logging | GitHub/GitLab audit logs |

## Troubleshooting Common Git Issues

### SSH Connection Problems
```bash
# Debug SSH connection to GitHub
ssh -vT git@github.com

# Test specific key
ssh -i ~/.ssh/github_ed25519 -T git@github.com

# Fix SSH agent issues
eval "$(ssh-agent -s)"
ssh-add ~/.ssh/github_ed25519
ssh-add -l  # List loaded keys

# Check SSH config
cat ~/.ssh/config
```

### Git Authentication Issues
```bash
# Switch remote from HTTPS to SSH
git remote set-url origin git@github.com:username/repository.git

# Fix credential helper issues
git config --global --unset credential.helper
git config --global credential.helper cache

# Clear cached credentials
git credential-manager-core erase
```

### Repository Synchronization
```bash
# Fix diverged branches
git pull --rebase origin main

# Reset to match remote
git fetch origin
git reset --hard origin/main

# Sync fork with upstream
git remote add upstream git@github.com:original/repository.git
git fetch upstream
git checkout main
git merge upstream/main
git push origin main
```

## Lab Exercises

### Lab 1: SSH Key Setup and GitHub Integration
**Objective:** Generate and register SSH keys with GitHub for secure Git operations

**Tasks:**
1. Generate ED25519 SSH key pair for GitHub access
2. Configure SSH agent and add key with proper security settings
3. Register public key with GitHub and verify connection
4. Set up SSH config for multiple GitHub accounts if needed
5. Test SSH authentication and troubleshoot any issues

**Deliverables:**
- Working SSH authentication to GitHub
- Documented SSH configuration
- Key management procedures

### Lab 2: Repository Creation and Clone Operations
**Objective:** Create and clone repositories using SSH URLs

**Tasks:**
1. Create new repository on GitHub with proper initialization
2. Clone repository using SSH URL
3. Configure local repository with user identity and settings
4. Set up multiple remotes (origin and upstream for forks)
5. Demonstrate different clone options (shallow, specific branch)

**Deliverables:**
- Successfully cloned and configured repository
- Multiple remote configurations
- Clone operation documentation

### Lab 3: Git Workflow Mastery
**Objective:** Perform essential Git operations with confidence

**Tasks:**
1. Practice staging, committing, and pushing changes
2. Create and manage feature branches
3. Perform merge and rebase operations
4. Handle merge conflicts resolution
5. Use Git history navigation and inspection commands

**Deliverables:**
- Complete feature branch workflow
- Merge conflict resolution examples
- Git history analysis and navigation

### Lab 4: Git Configuration and Customization
**Objective:** Master .git/config management and customization

**Tasks:**
1. Analyze and understand .git/config structure
2. Configure global and local Git settings
3. Create useful aliases for common operations
4. Set up custom merge and diff tools
5. Configure credential helpers and security settings

**Deliverables:**
- Optimized Git configuration setup
- Custom alias library
- Security-hardened Git settings

### Lab 5: Advanced .gitignore Management
**Objective:** Create comprehensive .gitignore strategies

**Tasks:**
1. Create project-specific .gitignore files for different technologies
2. Set up global .gitignore for system-wide exclusions
3. Implement .gitignore patterns for infrastructure projects
4. Use .gitignore API and tools for template generation
5. Audit existing repositories for ignored file coverage

**Deliverables:**
- Comprehensive .gitignore templates
- Global ignore configuration
- .gitignore management tools

### Lab 6: Professional Git Collaboration Workflow
**Objective:** Implement professional Git workflows and best practices

**Tasks:**
1. Set up feature branch workflow with proper naming conventions
2. Implement conventional commit message standards
3. Create and manage releases with proper tagging
4. Set up code review process with pull requests
5. Implement branch protection and automated workflows

**Deliverables:**
- Complete collaboration workflow documentation
- Automated workflow scripts
- Code review and quality standards

## Assessment Criteria

Each lab will be evaluated based on:

| Criteria | Weight | Description |
|----------|---------|-------------|
| Technical Implementation | 30% | Correct Git operations and SSH setup |
| Security Best Practices | 25% | Proper key management and secure workflows |
| Workflow Efficiency | 25% | Effective use of Git features and automation |
| Documentation Quality | 20% | Clear documentation and procedures |

## Next Steps

With Git and GitHub mastery achieved, you now have the foundational version control skills necessary for infrastructure automation. This knowledge directly supports the advanced DevOps workflows covered in Module 14 (Proxmox Infrastructure Automation), where you'll use Git repositories to manage Terraform configurations, Ansible playbooks, and Cloud-Init templates in a complete Infrastructure as Code (IaC) pipeline.

The SSH and security practices learned here also complement Module 13 (OpenSSH Best Practices) for comprehensive security across your infrastructure management toolkit.
