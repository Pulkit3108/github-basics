# Git Configuration Guide: Managing Multiple GitHub Accounts

## Overview

This guide helps you properly configure Git to manage multiple GitHub accounts (personal and professional) without mixing up commits. Proper Git configuration prevents email and name exposure issues that can lead to tangled commit histories.

## Table of Contents

- [GitHub Email Privacy Settings](#github-email-privacy-settings)
- [Basic Git Configuration](#basic-git-configuration)
- [Conditional Git Configurations](#conditional-git-configurations)
- [SSH Key Management](#ssh-key-management)
- [SSH Configuration](#ssh-configuration)
- [Usage](#usage)
- [Troubleshooting](#troubleshooting)

## GitHub Email Privacy Settings

### Step 1: Enable Email Privacy
1. Go to GitHub Settings → Emails
2. Check "Keep my email addresses private"
3. Copy your noreply email (displayed in bold)
4. Use this noreply email in your Git configurations

This ensures GitHub uses your noreply email instead of your actual email address in commits.

## Basic Git Configuration

### Check Current Configuration
```bash
git config --show-origin --get user.name
git config --show-origin --get user.email
```

### Set Global Configuration
```bash
git config --global user.name "Your Name"
git config --global user.email "your-noreply@users.noreply.github.com"
```

## Conditional Git Configurations

Create separate configurations for different project directories using conditional includes.

### Main Git Configuration (`~/.gitconfig`)
```ini
[includeIf "gitdir:/home/USERNAME/codes/github/personal/"]
    path = /home/USERNAME/.gitconfig-personal

[includeIf "gitdir:/home/USERNAME/codes/github/official/"]
    path = /home/USERNAME/.gitconfig-official
```

### Personal Configuration (`~/.gitconfig-personal`)
```ini
[user]
    name  = Your Personal Name
    email = personal-noreply@users.noreply.github.com
```

### Professional Configuration (`~/.gitconfig-official`)
```ini
[user]
    name  = Your Professional Name
    email = professional-noreply@users.noreply.github.com
```

## SSH Key Management

### Generate SSH Keys
Create separate SSH keys for each account:

```bash
# Personal account
ssh-keygen -t ed25519 -C "personal-noreply@users.noreply.github.com" -f ~/.ssh/id_ed25519_personal

# Professional account
ssh-keygen -t ed25519 -C "professional-noreply@users.noreply.github.com" -f ~/.ssh/id_ed25519_official
```

### Add Public Keys to GitHub
1. Copy the content of `~/.ssh/id_ed25519_personal.pub` and `~/.ssh/id_ed25519_official.pub`
2. Add them to the respective GitHub accounts under Settings → SSH and GPG keys

## SSH Configuration

Create an SSH config file (`~/.ssh/config`) to manage multiple identities:

```ssh
# Personal GitHub account
Host github-personal
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_personal
  IdentitiesOnly yes

# Official GitHub account
Host github-official
  HostName github.com
  User git
  IdentityFile ~/.ssh/id_ed25519_official
  IdentitiesOnly yes
```

## Usage

### Directory Structure
Organize your projects in separate directories:
```
/home/USERNAME/codes/github/
├── personal/
│   ├── project1/
│   └── project2/
└── official/
    ├── work-project1/
    └── work-project2/
```

### Cloning Repositories
Use the SSH host aliases defined in your config:

```bash
# Personal repository
git clone git@github-personal:username/repo-name.git

# Professional repository
git clone git@github-official:username/repo-name.git
```

### Adding Remote Origins
```bash
# Personal
git remote add origin git@github-personal:username/repo-name.git

# Professional
git remote add origin git@github-official:username/repo-name.git
```

## Troubleshooting

### Email Mismatch Alerts
If you try to commit with the wrong identity, Git will alert you about email mismatches, helping prevent mixed commits.

### Refresh Configuration
After making changes, restart your terminal or run:
```bash
exec $SHELL
```

### Verify Configuration
Check which configuration is being used in a specific repository:
```bash
git config user.name
git config user.email
```

## Important Notes

- Always use GitHub's noreply email addresses
- Keep personal and professional projects in separate directories
- The conditional configuration automatically applies the correct identity based on the project location
- SSH configuration prevents commits from the wrong identity
- If you have existing tangled commits, consider starting fresh with new repositories

## Contributing

If you have suggestions for improving this configuration setup, please feel free to submit issues or pull requests.

## License

This guide is provided as-is for educational purposes.
