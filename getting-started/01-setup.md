# GitHub Copilot Setup & Installation

## Prerequisites

- **Visual Studio Code** (v1.70+) or other supported IDE
- **GitHub Account** with Copilot subscription
- **Node.js** (for development environments)
- **Git** (for version control)

## Installation Steps

### 1. Install GitHub Copilot Extension

#### VS Code
```bash
# Via VS Code Extensions Marketplace
1. Open VS Code
2. Go to Extensions (Ctrl+Shift+X / Cmd+Shift+X)
3. Search for "GitHub Copilot"
4. Click Install on the official GitHub extension

# Or via command line
code --install-extension GitHub.copilot
```

#### Other IDEs
- **JetBrains IDEs** (IntelliJ, PyCharm, etc.)
- **Neovim** via plugin
- **Visual Studio** (Windows)
- Check GitHub Copilot documentation for your IDE

### 2. Authenticate

```bash
# GitHub CLI authentication
gh auth login

# VS Code will prompt for authentication
# Or use: GitHub Copilot: Sign In command
```

### 3. Verify Installation

```bash
# Check GitHub CLI integration
gh copilot --version

# Test Copilot in VS Code
# Open any file and start typing a comment
# Copilot should suggest completions
```

## Configuration Files

### .copilotignore (Optional)

Create in project root to exclude files from Copilot context:

```
node_modules/
dist/
build/
.env
secrets/
*.key
```

### VS Code Settings

Create `.vscode/settings.json`:

```json
{
  "github.copilot.enable": {
    "*": true,
    "plaintext": false,
    "markdown": true
  },
  "github.copilot.advanced": {
    "debug.overrideCacheForDebugging": false,
    "debug.testOverrideProxyUrl": "",
    "debug.testOverrideToken": "",
    "debug.overrideEngine": "",
    "authProvider": "github"
  }
}
```

## First-Time Setup Checklist

- [ ] GitHub Copilot extension installed
- [ ] GitHub authentication completed
- [ ] Copilot suggestions appearing in editor
- [ ] `.vscode/settings.json` configured (optional)
- [ ] `.copilotignore` file created if needed
- [ ] Team policies documented (if applicable)

## Troubleshooting

### Copilot Not Working
- Verify GitHub CLI: `gh auth status`
- Check VS Code version: `code --version`
- Restart VS Code
- Clear cache: Delete `.vscode` folder and restart

### Authentication Issues
- Re-authenticate: `gh auth logout && gh auth login`
- Check GitHub token permissions
- Ensure GitHub Copilot subscription is active

### No Suggestions Appearing
- Check file type (Copilot works best with code files)
- Verify `github.copilot.enable` settings
- Start typing comments or function signatures
- File may be in `.copilotignore`

## Team Setup

### Enterprise Configuration
1. Contact GitHub for enterprise licensing
2. Set organizational policies
3. Configure SAML/SSO if needed
4. Set up team access controls

### Company Policies
- Define acceptable use policies
- Document code review requirements
- Establish security guidelines
- Create team prompts library

---

**Next Step**: [First Steps with Copilot](./02-first-steps.md)
