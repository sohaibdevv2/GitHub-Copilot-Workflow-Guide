# First Steps with GitHub Copilot

## Your First Copilot Suggestions

### Start Simple: Line Completion

Open any JavaScript file and type:

```javascript
function calculateTotal(items) {
  // C
```

When you type the comment, Copilot will suggest completions. Hit `Tab` to accept.

### Function Generation

Start typing a function signature:

```javascript
function fetchUserData(userId) {
  // Copilot suggests the implementation
}
```

### Understanding Suggestions

- **Gray text** = Copilot's suggestion
- **Tab key** = Accept suggestion
- **Esc key** = Reject suggestion
- **Alt+[ / Alt+]** = Cycle through alternatives
- **Ctrl+Enter** = Open suggestion panel (up to 10 options)

## Common First Tasks

### 1. Generate a Function
```javascript
// Write a function to validate email addresses
function validateEmail(email) {
  
}
```

Position cursor inside the function. Copilot will suggest validation logic.

### 2. Write Comments First (Best Practice)

```javascript
// Convert array of objects to a map with id as key
function arrayToMap(items) {
  
}
```

Clear comments help Copilot understand your intent better.

### 3. Generate Tests

```javascript
// Test that validateEmail returns true for valid emails
function testValidateEmail() {
  
}
```

### 4. Refactor Code

Select existing code and comment above it:

```javascript
// Simplify this using modern JavaScript
```

Copilot will suggest refactored versions.

## Best Practices from Day One

### ✅ DO

- **Use clear comments** — Describe what you want
- **Be specific** — More detail = better suggestions
- **Review suggestions** — Always read generated code
- **Iterate** — Refine your request if needed
- **Ask for style** — Specify coding style preferences

### ❌ DON'T

- **Accept blindly** — Always review code
- **Skip testing** — Test Copilot-generated code
- **Use for secrets** — Never commit sensitive data
- **Rely entirely** — Use Copilot as an assistant, not replacement
- **Ignore warnings** — Pay attention to linting/type errors

## Keyboard Shortcuts

| Action | Shortcut |
|--------|----------|
| Accept suggestion | `Tab` |
| Reject suggestion | `Esc` |
| Next suggestion | `Alt+]` |
| Previous suggestion | `Alt+[` |
| Open suggestion panel | `Ctrl+Enter` |
| Trigger inline chat | `Ctrl+I` |

## Your First Session

1. **Open a simple project file**
2. **Start with comments** describing what you want
3. **Let Copilot suggest** the next line/function
4. **Review the suggestion** carefully
5. **Accept, modify, or reject** the suggestion
6. **Test the code** to verify it works

## Common Beginner Mistakes

| Mistake | Fix |
|---------|-----|
| Vague comments | Be specific: `// Calculate sum of positive numbers` |
| Accepting all suggestions | Review first, then accept |
| Not testing generated code | Always run tests |
| Complex requests | Break into smaller steps |
| Ignoring context | Provide enough context in comments |

## Mental Model

Think of Copilot as a **very smart autocomplete** that:
- Understands code context
- Knows common patterns
- Learns from your project structure
- Works best with clear instructions

It's **not** a replacement for developers—it's a tool to make you faster.

## Next: Improve Your Skills

- Learn [Prompting Techniques](../core-concepts/03-prompting-techniques.md)
- Explore [Code Generation Patterns](../core-concepts/04-code-generation-patterns.md)
- Try [Rapid Development Workflow](../workflows/01-rapid-development.md)

---

**Previous**: [Setup & Installation](./01-setup.md)  
**Next**: [Configuration Guide](./03-configuration.md)
