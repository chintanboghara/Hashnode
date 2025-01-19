---
title: "GitHub CLI"
seoTitle: "GitHub Command Line Tool"
seoDescription: "Explore GitHub CLI: a command-line tool to manage GitHub repositories, issues, pull requests, and workflows efficiently from your terminal"
datePublished: Sat Jan 04 2025 03:30:51 GMT+0000 (Coordinated Universal Time)
cuid: cm5hmmkiq000909mefto21nym
slug: github-cli
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1737266760449/11504d2b-0a74-4d2d-921d-abc554e76143.png
tags: cloud, github, devops, sre, devsecops, github-cli, platform-engineering

---

## About the GitHub CLI

GitHub CLI is a command-line tool that brings pull requests, issues, GitHub Actions, and other GitHub features to your terminal, allowing you to do all your work in one place.

**GitHub CLI includes features like:**

* View, create, clone, and fork repositories
    
* Create, close, edit, and view issues and pull requests
    
* Review, compare, and merge pull requests
    
* Run, view, and list workflows
    
* Create, list, view, and delete releases
    
* Create, edit, list, view, and delete gists
    
* List, create, delete, and connect to a codespace
    
* Retrieve information from the GitHub API
    

## What is the difference between GitHub CLI and Git on the command line?

The Git command line interface (`git`) lets you work with a local or remote Git repository. The remote repository can be hosted on GitHub or another service.

GitHub CLI (`gh`) is designed specifically for working with GitHub. It enables you to interact with GitHub through the command line in various ways, as shown in the previous list. If you often work on the command line, you might prefer using GitHub CLI instead of accessing GitHub through a browser. GitHub CLI also simplifies creating scripts to automate GitHub tasks.

## Installing GitHub CLI

For instructions on how to install GitHub CLI, visit the [GitHub CLI repository](https://github.com/cli/cli#installation) and [GitHub CLI](https://cli.github.com/).

![Command prompt showing the GitHub CLI version as 2.64.0 with a release date of 2024-12-20 and a URL link to its release page.](https://cdn.hashnode.com/res/hashnode/image/upload/v1735956244794/5b78dc70-0784-4ead-afda-9f5f8b24ecb0.png align="center")

## gh

Work smoothly with GitHub using the command line.

### gh auth

Authenticate `gh` and `git` with GitHub

* [gh auth login](https://cli.github.com/manual/gh_auth_login)
    
* [gh auth logout](https://cli.github.com/manual/gh_auth_logout)
    
* [gh auth refresh](https://cli.github.com/manual/gh_auth_refresh)
    
* [gh auth setup-git](https://cli.github.com/manual/gh_auth_setup-git)
    
* [gh auth status](https://cli.github.com/manual/gh_auth_status)
    
* [gh auth switch](https://cli.github.com/manual/gh_auth_switch)
    
* [gh auth token](https://cli.github.com/manual/gh_auth_token)
    

![A terminal window displaying a GitHub authentication process. The user is prompted to select their GitHub usage, protocol preference, and authentication method. A one-time code is provided, with instructions to open a login URL in a browser.](https://cdn.hashnode.com/res/hashnode/image/upload/v1735956578316/fff40388-8632-435c-a182-1ad36e4e2004.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1735956583272/bc5f2f31-d2b4-4324-b76b-d1948e833ddd.png align="center")

![Terminal screenshot showing GitHub authentication steps. It includes a one-time code, authentication confirmation, and successful login message.](https://cdn.hashnode.com/res/hashnode/image/upload/v1735956705514/a66bfd42-1f20-49eb-9c78-92dc27747b0f.png align="center")

![Command prompt showing GitHub authentication status and refresh process, with details about the account, token scopes, and a one-time code for logging in.](https://cdn.hashnode.com/res/hashnode/image/upload/v1735957095324/bd27b5a1-595f-444f-b753-87da799591dc.png align="center")

## **Core Commands**

These commands help you manage repositories, issues, pull requests, and other key features of GitHub.

1. `gh browse`  
    Open a GitHub repository, issue, pull request, or discussion in your browser.
    
2. `gh codespace`  
    Work with GitHub Codespaces, including creating, managing, or connecting to a codespace.
    
3. `gh gist`  
    Create, list, edit, or delete GitHub gists.
    
4. `gh issue`  
    Manage GitHub issues: create, view, close, reopen, or comment on issues.
    
5. `gh org`  
    Manage GitHub organizations: list members, view details, and more.
    
6. `gh pr`  
    Manage pull requests: create, view, merge, close, or comment on pull requests.
    
7. `gh project`  
    Work with GitHub Projects: manage project boards and items.
    
8. `gh release`  
    Manage releases: create, edit, delete, or download release assets.
    
9. `gh repo`  
    Interact with GitHub repositories: clone, fork, create, delete, or view information about repositories.
    

## **GitHub Actions Commands**

These commands are designed to automate workflows and manage GitHub Actions.

1. `gh cache`  
    Manage GitHub Actions cache: list, delete, or view cache details.
    
2. `gh run`  
    View, monitor, or manage GitHub Actions workflow runs.
    
3. `gh workflow`  
    Manage workflows: enable, disable, view, or rerun them.
    

## **Additional Commands**

These commands handle various administrative, configuration, and utility tasks.

1. `gh alias`  
    Create or manage command shortcuts for the GitHub CLI.
    
2. `gh api`  
    Make direct requests to the GitHub API.
    
3. `gh attestation`  
    Manage security attestations for GitHub releases or artifacts.
    
4. `gh completion`  
    Generate shell completion scripts for the GitHub CLI.
    
5. `gh config`  
    Manage GitHub CLI settings, including authentication and preferences.
    
6. `gh extension`  
    Install, manage, or create GitHub CLI extensions.
    
7. `gh gpg-key`  
    Manage GPG keys: list, add, or delete keys linked to your GitHub account.
    
8. `gh label`  
    Manage repository labels: create, edit, or delete them.
    
9. `gh ruleset`  
    Work with GitHub's repository or organization rulesets.
    
10. `gh search`  
    Search for repositories, issues, pull requests, and more.
    
11. `gh secret`  
    Manage GitHub Secrets for repositories or environments.
    
12. `gh ssh-key`  
    Manage SSH keys: list, add, or delete keys linked to your GitHub account.
    
13. `gh status`  
    Display the current status of GitHub services.
    
14. `gh variable`  
    Manage environment variables for GitHub Actions.
    

**Need Help?**

For any of these commands, use the `--help` flag to see details about usage. For example:

```bash
gh repo --help
```

**Examples**

```bash
$ gh issue create
$ gh repo clone cli/cli
$ gh pr checkout 321
```

## References

1. **GitHub CLI Repository**  
    [https://github.com/cli/cli](https://github.com/cli/cli)
    
2. **GitHub CLI Installation Instructions**  
    [https://cli.github.com](https://cli.github.com/)