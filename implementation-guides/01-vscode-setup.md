# GitHub Copilot Implementation Guide for VS Code

## Pre-Installation Requirements

- **VS Code**: v1.70 or later
- **GitHub Account**: Active, with Copilot subscription
- **Node.js** (optional): For testing Copilot with JavaScript

## Step-by-Step Installation

### Step 1: Install GitHub Copilot Extension

1. **Open VS Code**
2. **Go to Extensions** (Ctrl+Shift+X / Cmd+Shift+X)
3. **Search for** "GitHub Copilot"
4. **Click Install** on the official GitHub extension

```
Official Extension: GitHub Copilot
Publisher: GitHub
Version: Latest
```

### Step 2: Install Copilot Chat (Optional but Recommended)

Same process:
- Search for "GitHub Copilot Chat"
- Click Install

## Step 3: Authenticate

### Via GitHub CLI (Recommended)

```bash
# Authenticate with GitHub
gh auth login

# Follow prompts:
# - Protocol: HTTPS
# - Authentication: GitHub.com
# - Allow git to use credentials: Yes
```

### Via VS Code UI

1. Open VS Code Command Palette (Ctrl+Shift+P)
2. Type "GitHub Copilot: Sign In"
3. Browser opens for authentication
4. Approve permissions
5. Return to VS Code

## Step 4: Verify Installation

### Verify Extension

```bash
# Check installed extensions
code --list-extensions | grep copilot
```

Should output:
```
github.copilot
github.copilot-chat
```

### Test Copilot

1. Create a new JavaScript file: `test.js`
2. Type a comment:
   ```javascript
   // Calculate the sum of an array
   ```
3. Press Enter and start typing `function`
4. Copilot should suggest completions

## Configure VS Code Settings

### Open Settings File

Press `Ctrl+Shift+P`, type "Preferences: Open Settings (JSON)"

### Recommended Settings

```json
{
  // Copilot Settings
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": false
  },
  
  "github.copilot.inlineSuggest.enabled": true,
  "github.copilot.advanced": {
    "authProvider": "github"
  },

  // Editor Improvements
  "editor.formatOnSave": true,
  "editor.defaultFormatter": "esbenp.prettier-vscode",
  
  // TypeScript
  "typescript.tsdk": "node_modules/typescript/lib",
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode"
  },

  // Python (if applicable)
  "[python]": {
    "editor.defaultFormatter": "ms-python.python"
  }
}
```

## Setup Project-Level Configuration

### Create VS Code Workspace Settings

1. Create `.vscode` folder in project root
2. Create `.vscode/settings.json`:

```json
{
  "github.copilot.enable": {
    "*": true
  },
  "[typescript]": {
    "editor.formatOnSave": true
  }
}
```

### Create Extensions Recommendations

Create `.vscode/extensions.json`:

```json
{
  "recommendations": [
    "GitHub.copilot",
    "GitHub.copilot-chat",
    "ms-python.python",
    "esbenp.prettier-vscode",
    "dbaeumer.vscode-eslint"
  ]
}
```

## Setup Keyboard Shortcuts (Optional)

Create custom keybindings in `.vscode/keybindings.json`:

```json
[
  {
    "key": "alt+/",
    "command": "editor.action.inlineSuggest.trigger",
    "when": "editorTextFocus && !editorReadonly"
  },
  {
    "key": "ctrl+alt+enter",
    "command": "github.copilot.openSymbolFromEditor",
    "when": "editorTextFocus"
  }
]
```

## Create Project `.copilotignore`

In project root:

```
# Environment Files
.env
.env.local
.env.*.local
secrets/
*.key
*.pem

# Dependencies & Build
node_modules/
dist/
build/
.next/

# Generated Files
*.generated.*
coverage/
.tsbuildinfo

# Version Control
.git/

# IDE
.vscode/
.idea/

# OS
.DS_Store
Thumbs.db
```

## Team Setup

### Share Configuration

```bash
# Commit to repository
git add .vscode/
git add .copilotignore
git commit -m "chore: add Copilot configuration for team"
```

### Create CLAUDE.md

```markdown
# [Project Name] — Copilot Configuration

## Copilot is Enabled

All developers should use GitHub Copilot for this project.

### Setup Instructions
1. Install GitHub Copilot extension
2. Authenticate with GitHub
3. Review .copilotignore for excluded files
4. See best-practices for team standards

### Code Review
All Copilot-generated code must pass code review before merging.
```

## Troubleshooting Installation

### Issue: "GitHub Copilot is not authorized"

**Solution**:
```bash
# Re-authenticate
gh auth logout
gh auth login
# Restart VS Code
```

### Issue: "Extension failed to activate"

**Solution**:
1. Uninstall GitHub Copilot extension
2. Restart VS Code
3. Reinstall from marketplace

### Issue: "No suggestions appearing"

**Checklist**:
- [ ] File is not in `.copilotignore`
- [ ] Copilot is enabled in settings
- [ ] GitHub authentication successful
- [ ] File type is supported (not .txt)
- [ ] Start typing comments or code

### Issue: "Slow suggestions"

**Optimize**:
1. Exclude large files from `.copilotignore`
2. Close unnecessary editor tabs
3. Clear VS Code cache: `code --profile delete default`
4. Restart VS Code

## Verify Complete Setup

### Checklist

```
Installation:
  ✓ GitHub Copilot extension installed
  ✓ GitHub authentication complete
  ✓ Copilot suggestions working

Configuration:
  ✓ VS Code settings configured
  ✓ .copilotignore created
  ✓ Project-level settings set up

Team:
  ✓ .vscode/ committed to repository
  ✓ CLAUDE.md created
  ✓ Team trained on usage
```

## Next Steps

1. **Learn**: Follow the [Getting Started](../getting-started) guide
2. **Practice**: Try [First Steps with Copilot](../getting-started/02-first-steps.md)
3. **Master**: Study [Prompting Techniques](../core-concepts/03-prompting-techniques.md)
4. **Scale**: Review [Team Standards](../best-practices/02-team-standards.md)

---

**Next**: [Git Integration](./02-git-integration.md)
