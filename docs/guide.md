# GitHub CLI (gh) User Guide

## Table of Contents
- [Introduction](#introduction)
- [Installation](#installation)
- [Authentication](#authentication)
- [Repository Management](#repository-management)
- [Pull Requests](#pull-requests)
- [Issues](#issues)
- [GitHub Actions](#github-actions)
- [Gists](#gists)
- [Advanced Features](#advanced-features)
- [Tips and Tricks](#tips-and-tricks)

## Introduction

GitHub CLI (`gh`) is a command-line tool that brings GitHub functionality to your terminal. It allows you to work with GitHub features like repositories, issues, and pull requests directly from your command line.

## Installation

### macOS
```bash
brew install gh
```

### Windows
```bash
winget install --id GitHub.cli
# or with Chocolatey
choco install gh
```

### Linux
```bash
# Debian/Ubuntu
sudo apt install gh

# Fedora
sudo dnf install gh
```

## Authentication

Before using GitHub CLI, you need to authenticate with your GitHub account.

```bash
# Start the authentication process
gh auth login

# Check authentication status
gh auth status

# Log out
gh auth logout
```

During authentication, you'll be asked:
1. Which GitHub host to use (github.com or enterprise)
2. Authentication protocol (HTTPS or SSH)
3. Authentication method (web browser, token, or SSH key)

## Repository Management

### Creating Repositories

```bash
# Create a new repository (interactive)
gh repo create

# Create a new public repository with a specific name
gh repo create my-project --public

# Create a repository from an existing local directory
gh repo create my-project --source=. --private
```

### Cloning Repositories

```bash
# Clone your own repository
gh repo clone my-project

# Clone someone else's repository
gh repo clone username/repo-name

# Clone with specific branch
gh repo clone username/repo-name -- -b branch-name
```

### Repository Information

```bash
# View repository details
gh repo view

# View repository details of a specific repo
gh repo view username/repo-name

# Open repository in browser
gh repo view --web

# List your repositories
gh repo list

# List repositories of an organization
gh repo list organization-name
```

### Repository Actions

```bash
# Fork a repository
gh repo fork username/repo-name

# Archive a repository
gh repo archive username/repo-name

# Delete a repository (requires confirmation)
gh repo delete username/repo-name
```

## Pull Requests

### Creating Pull Requests

```bash
# Create a pull request (interactive)
gh pr create

# Create a pull request with title and body
gh pr create --title "Fix bug" --body "This PR fixes a critical bug"

# Create a draft pull request
gh pr create --draft

# Create a pull request targeting a specific branch
gh pr create --base develop
```

### Managing Pull Requests

```bash
# List pull requests
gh pr list

# View a specific pull request
gh pr view 123

# Check out a pull request locally
gh pr checkout 123

# Approve a pull request
gh pr review 123 --approve

# Request changes on a pull request
gh pr review 123 --comment -b "Please fix these issues"

# Merge a pull request
gh pr merge 123

# Close a pull request without merging
gh pr close 123
```

### Pull Request Status

```bash
# Check PR status
gh pr status

# View CI status for a pull request
gh pr checks 123
```

## Issues

### Creating Issues

```bash
# Create an issue (interactive)
gh issue create

# Create an issue with title and body
gh issue create --title "Bug report" --body "Description of the bug"

# Create an issue with labels and assignees
gh issue create --label bug,urgent --assignee username1,username2
```

### Managing Issues

```bash
# List issues
gh issue list

# List closed issues
gh issue list --state closed

# View a specific issue
gh issue view 456

# Close an issue
gh issue close 456

# Reopen an issue
gh issue reopen 456

# Assign an issue
gh issue edit 456 --add-assignee username
```

### Issue Status

```bash
# Check issue status
gh issue status

# View all issues assigned to you
gh issue list --assignee @me
```

## GitHub Actions

```bash
# List workflows
gh workflow list

# View a specific workflow
gh workflow view workflow-name.yml

# Run a workflow
gh workflow run workflow-name.yml

# View workflow runs
gh run list

# View a specific run
gh run view run-id

# Download artifacts from a run
gh run download run-id
```

## Gists

```bash
# Create a gist from a file
gh gist create file.txt

# Create a private gist
gh gist create file.txt --private

# List your gists
gh gist list

# View a specific gist
gh gist view gist-id

# Edit a gist
gh gist edit gist-id
```

## Advanced Features

### GitHub CLI Extensions

GitHub CLI supports extensions that add new functionality:

```bash
# List available extensions
gh extension list

# Install an extension
gh extension install owner/name

# Update extensions
gh extension upgrade

# Create your own extension
gh extension create extension-name
```

### Aliases

Create custom shortcuts for common commands:

```bash
# Create an alias
gh alias set prc 'pr create --title "$1" --body "$2"'

# Use the alias
gh prc "Fix bug" "This fixes a critical bug"

# List aliases
gh alias list

# Delete an alias
gh alias delete prc
```

### Environment Variables

GitHub CLI uses several environment variables:

- `GH_TOKEN`: Authentication token
- `GH_HOST`: GitHub hostname
- `GH_REPO`: Default repository
- `GH_EDITOR`: Editor for authoring content

### API Access

Use the API command to make direct requests:

```bash
# GET request
gh api repos/owner/repo

# POST request with data
gh api repos/owner/repo/issues -F title="Bug" -F body="Description"

# PUT request
gh api repos/owner/repo/topics -F topics[]="topic1" -F topics[]="topic2"
```

## Tips and Tricks

### Output Formatting

Control output format for data:

```bash
# JSON output
gh issue list --json number,title,assignees

# Template-based output
gh issue list --json number,title --template '{{range .}}#{{.number}} {{.title}}{{end}}'
```

### Configuration

Manage configuration:

```bash
# Set a configuration value
gh config set editor vim

# Get a configuration value
gh config get editor

# List configuration
gh config list
```

### Searching

Search GitHub resources:

```bash
# Search repositories
gh search repos "machine learning"

# Search issues
gh search issues "bug in login"

# Search pull requests
gh search prs "fix documentation"
```

### Copilot in CLI

If you have GitHub Copilot, use it in the CLI:

```bash
# Ask Copilot a question
gh copilot suggest "How do I create a new branch?"

# Get command explanations
gh copilot explain "git rebase -i HEAD~3"
```

---

For more information, visit the [GitHub CLI documentation](https://cli.github.com/manual/) or run `gh help` for command-specific help.

