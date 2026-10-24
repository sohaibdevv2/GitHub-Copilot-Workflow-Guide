# Quick Start Reference & FAQ

## Quick Reference

### Most Common Tasks

| Task | Command/Pattern |
|------|-----------------|
| Accept suggestion | Press `Tab` |
| Reject suggestion | Press `Esc` |
| Cycle suggestions | `Alt+]` / `Alt+[` |
| Open suggestion panel | `Ctrl+Enter` |
| Generate test | Comment: `// Test that...` |
| Generate function | Comment: `// Function that...` |

### Common Prompts

```javascript
// Validation
// Validate email address format

// Transformation
// Convert array of objects to object keyed by id

// Formatting
// Format date as YYYY-MM-DD HH:MM:SS

// Sorting
// Sort array by property name ascending

// Grouping
// Group array of objects by status property
```

## FAQ

### Q1: Copilot isn't suggesting anything

**A**: Try:
- Type more descriptive comment
- Ensure file type is supported (not .txt)
- Check GitHub authentication: `gh auth status`
- Restart VS Code
- Check that Copilot is enabled in settings

### Q2: Suggestions are wrong or poor quality

**A**: Improve context:
- Add type definitions
- Use more specific comments
- Show examples
- Open related files
- Establish patterns first

### Q3: Can I use Copilot for security-sensitive code?

**A**: **Not recommended without review**:
- Always have security expert review
- Don't use for cryptography implementation
- Don't use for authentication logic without review
- Use for boilerplate after security review

### Q4: Does Copilot learn from my code?

**A**: Depends on your settings:
- Personal: Default uses your code for training
- Enterprise: Can opt out entirely
- Check GitHub's privacy policy
- Use `.copilotignore` for sensitive code

### Q5: How do I contribute to team standards?

**A**: Create `CLAUDE.md`:
```markdown
# Project Standards for Copilot

## Naming Conventions
- Functions: camelCase
- Classes: PascalCase
- Constants: UPPER_SNAKE_CASE

## Code Style
- Use async/await, not callbacks
- Prefer functional over imperative
- Always include error handling
```

### Q6: Can Copilot refactor existing code?

**A**: Yes:
1. Select code
2. Comment: `// Refactor this using modern JavaScript`
3. Let Copilot suggest improvements
4. Review and accept/reject

### Q7: Best practice for reviewing Copilot code?

**A**: Use checklist:
- [ ] Does it solve the stated problem?
- [ ] Does it follow project style?
- [ ] Are there any obvious bugs?
- [ ] Is performance acceptable?
- [ ] Is error handling complete?
- [ ] Would you approve this in code review?

### Q8: How to speed up development with Copilot?

**A**: 
1. **Structure first** — Set up files/folders
2. **Types first** — Define interfaces/types
3. **Pattern first** — Establish one good example
4. **Generate** — Let Copilot complete similar tasks
5. **Review & merge** — Spot check quality

---

**Go back**: [Main Guide](../README.md)
