# GitHub Copilot Configuration Guide

## VS Code Settings

### Basic Configuration

Create or update `.vscode/settings.json`:

```json
{
  // Enable/disable Copilot by file type
  "github.copilot.enable": {
    "*": true,
    "yaml": false,
    "plaintext": false,
    "markdown": false
  },
  
  // Copilot Chat settings
  "github.copilot.chat.autocomplete": true,
  
  // Inline suggestions
  "github.copilot.inlineSuggest.enabled": true
}
```

### Advanced Settings

```json
{
  "github.copilot.advanced": {
    "authProvider": "github",
    "listAllowlistWhenInvokedWithoutQuery": false,
    "listMaxResults": 10,
    "debug.testOverrideProxyUrl": "",
    "debug.overrideCacheForDebugging": false,
    "telemetry.level": "all"
  }
}
```

## Team Configuration

### Create Team Settings

Store in `.vscode/settings.json` in your repository root:

```json
{
  // Team-wide Copilot settings
  "github.copilot.enable": {
    "*": true
  },
  
  // Disable for sensitive files
  "files.exclude": {
    "**/.env": true,
    "**/secrets": true
  }
}
```

### Recommended Extensions

```json
{
  "recommendations": [
    "GitHub.copilot",
    "GitHub.copilot-chat",
    "ms-python.python",
    "esbenp.prettier-vscode"
  ]
}
```

Add to `.vscode/extensions.json`

## Project-Level Control

### .copilotignore

Create in project root:

```
# Environment & secrets
.env
.env.local
.env.*.local
secrets/
*.key
*.pem

# Dependencies
node_modules/
venv/
__pycache__/

# Build outputs
dist/
build/
.next/
out/

# Generated files
*.generated.*

# Sensitive directories
private/
internal/
```

### CLAUDE.md Configuration

Create `CLAUDE.md` for project-specific guidance:

```markdown
# [Project Name] — Copilot Configuration

## Architecture
[Describe your project structure]

## Key Files
- `src/config.ts` — Configuration
- `src/types/index.ts` — Type definitions
- `tests/` — Test patterns

## Code Standards
- Use TypeScript
- Follow ESLint config
- Write tests for new features

## Copilot Guidelines
- Always code review AI suggestions
- Run tests before committing
- Use specific comments for better suggestions

## NEVER
- Commit secrets or API keys
- Use Copilot for security-critical code without review
- Skip testing
```

## Language-Specific Configuration

### Python

```json
{
  "python.linting.enabled": true,
  "python.linting.pylintEnabled": true,
  "[python]": {
    "editor.formatOnSave": true,
    "editor.defaultFormatter": "ms-python.python"
  }
}
```

### JavaScript/TypeScript

```json
{
  "[javascript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  "[typescript]": {
    "editor.defaultFormatter": "esbenp.prettier-vscode",
    "editor.formatOnSave": true
  },
  "typescript.tsdk": "node_modules/typescript/lib"
}
```

### Java

```json
{
  "[java]": {
    "editor.defaultFormatter": "redhat.java",
    "editor.formatOnSave": true
  }
}
```

## Telemetry & Privacy

### Disable Telemetry

```json
{
  "github.copilot.advanced": {
    "telemetry.level": "off"
  }
}
```

### Privacy Considerations

- Copilot doesn't store your code
- Your code is used to improve the model (unless opted out)
- Enterprise customers can opt out of data usage
- Always use `.copilotignore` for sensitive code

## Performance Optimization

### For Large Projects

```json
{
  "github.copilot.inlineSuggest.enabled": true,
  "github.copilot.enable": {
    "*": true,
    "*.test.ts": false,
    "*.spec.ts": false
  }
}
```

### Reduce Latency

- Exclude unnecessary files in `.copilotignore`
- Disable on large binary/generated files
- Keep `.vscode` settings minimal

## Troubleshooting Configuration

### Check Current Settings
```bash
# View active settings
code --list-extensions

# Check VS Code configuration
cat ~/.config/Code/User/settings.json
```

### Reset Configuration
```bash
# Back up current settings
cp ~/.config/Code/User/settings.json ~/settings.backup.json

# Remove problematic settings
# Then restart VS Code
```

## Next Steps

- Review [Prompting Techniques](../core-concepts/03-prompting-techniques.md)
- Set up [Team Standards](../best-practices/02-team-standards.md)
- Explore [VS Code Setup Guide](../implementation-guides/01-vscode-setup.md)

---

**Previous**: [First Steps with Copilot](./02-first-steps.md)
