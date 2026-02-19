# Rofi Launcher Scripts

A collection of rofi-based launcher scripts for GitHub workflow automation.

## Features

- **Smart Launcher** - Unified menu for quick access to GitHub tools
- **GitHub Issues** - View issues assigned to you
- **Pull Requests** - Browse your created PRs and review requests
- **Repository Selection** - Quickly switch between repositories you have access to

## Requirements

- `rofi` - Window menu and dmenu clone
- `gh` - GitHub CLI with authenticated session
- `bash` - Shell interpreter
- `xdg-open` - Used to open URLs in default browser

## Installation

1. Clone or download the scripts to your desired location:
```bash
git clone <repo-url> ~/.config/horroko-dev/rofi-launcher-scripts
```

2. Ensure all scripts are executable:
```bash
chmod +x ~/.config/horroko-dev/rofi-launcher-scripts/*
```

3. Verify `gh` CLI is installed and authenticated:
```bash
gh auth login
```

## Configuration

Configuration is stored in `~/.config/horroko-dev/rofi-git-issue.conf`:

```bash
# GitHub repository for rofi-git-issue
# Format: owner/repo
GITHUB_REPOSITORY="horroko-dev/rofi-launcher-scripts"
```

You can change the active repository using the smart launcher's "sr (select repository)" option.

## Usage

### Smart Launcher

The main entry point for all functionality. Accessible via Super+Enter (if configured in niri).

Menu options:
- **ghn** - Show GitHub notifications (inbox notifications)
- **ghi** - Show my GitHub issues (issues assigned to you)
- **ghprc** - Show created PRs (pull requests you created)
- **ghprr** - Show review requests (PRs requesting your review)
- **ghsr** - Select repository (switch active repository)

### Individual Scripts

Each function can also be run directly:

```bash
./rofi-smart-launcher      # Main menu
./rofi-notifications      # Show GitHub notifications
./rofi-git-issue          # Show assigned issues
./rofi-git-pr-created     # Show your PRs
./rofi-git-pr-review      # Show review requests
./rofi-select-repo        # Select active repository
```

### Window Manager Integration

You can bind the smart launcher to a keyboard shortcut in your window manager. For example:

**Niri:**
```kdl
Super+Return { spawn "/home/rk/git/horroko-dev/rofi-launcher-scripts/rofi-smart-launcher"; }
```

**I3/Sway:**
```
bindsym $mod+Return exec /home/rk/git/horroko-dev/rofi-launcher-scripts/rofi-smart-launcher
```

**Other WMs:**
Refer to your window manager's documentation for binding custom commands to keyboard shortcuts.

## How It Works

### GitHub Issues (`rofi-git-issue`)
- Fetches all issues assigned to the authenticated user
- Displays them in rofi with format: `owner/repo: #123 Issue title`
- Clicking/selecting an issue opens it in your default browser

### Created PRs (`rofi-git-pr-created`)
- Fetches all pull requests created by the authenticated user
- Displays them with repository prefix for easy identification
- Opens selected PR in browser

### Review Requests (`rofi-git-pr-review`)
- Fetches all PRs where you have been requested to review
- Searches across the configured repository
- Opens selected PR in browser

### GitHub Notifications (`rofi-notifications`)
- Fetches all unread notifications from your GitHub inbox
- Displays notification reason and title (e.g., "[review_requested] PR title")
- Automatically marks notification as read when opened
- Opens the notification URL in your default browser
- Supports all notification reasons: review requests, mentions, comments, assignments, etc.

### Repository Selection (`rofi-select-repo`)
- Lists all repositories you have access to (personal + organization repos)
- Uses GitHub GraphQL API to fetch org repositories
- Updates the config file when a repository is selected
- Affects all other scripts immediately (they read the config on each run)

## Troubleshooting

### Lists appear empty
- Verify `gh` is authenticated: `gh auth status`
- Check your GitHub permissions for the repository
- Ensure the repository name in config is correct

### Repository prefix not showing
- This is expected behavior if you have multiple repos configured
- The prefix helps identify which repo each item belongs to

### Scripts not executable
```bash
chmod +x ~/.config/horroko-dev/rofi-launcher-scripts/*
```

### Rofi not opening
- Ensure rofi is installed: `which rofi`
- Check if the script has execute permissions
- Verify the script path is correct in niri config

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
