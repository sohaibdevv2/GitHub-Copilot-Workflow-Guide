# Common Pitfalls & How to Avoid Them

## Pitfall 1: Blind Acceptance

### ❌ The Problem
```javascript
// Just accept every suggestion without reviewing
function processUser(user) {
  // Copilot suggests something, hit Tab
  // Don't read it, move on
}
```

### ✅ The Solution
- Always review before accepting
- Read the entire suggestion
- Ask "Does this make sense?"
- Run tests after accepting

### Prevention
```javascript
Create a checklist:
[ ] Reviewed the suggestion
[ ] Tested the code
[ ] Matches project style
[ ] No obvious bugs
```

---

## Pitfall 2: Poor Context

### ❌ The Problem
```javascript
// Vague prompt
function process() {
  // Copilot confused about what to do
}
```

### ✅ The Solution
```javascript
// Specific prompt with context
function processUserPayment(user, amount) {
  // Calculate final amount including tax
  // Return object with {subtotal, tax, total}
}
```

### Prevention
- Use descriptive function names
- Add type definitions
- Write clear comments
- Establish patterns first

---

## Pitfall 3: Security Issues

### ❌ The Problem
```python
# Copilot might suggest hardcoding or unsafe code
def get_database_connection():
    password = "hardcoded_password"  # ❌ Don't do this!
    return connect(password)
```

### ✅ The Solution
```python
# Use environment variables or secrets manager
import os
from cryptography import fernet

def get_database_connection():
    password = os.getenv('DB_PASSWORD')  # ✅ Correct
    return connect(password)
```

### Prevention
- Never paste credentials into Copilot
- Use `.copilotignore` for `.env` files
- Review auth-related code carefully
- Use secrets manager for production

---

## Pitfall 4: Over-Reliance

### ❌ The Problem
```
Team depends entirely on Copilot
Team forgets how to code without it
Skills atrophy
Quality suffers
```

### ✅ The Solution
- Use Copilot as assistant, not replacement
- Code some things manually
- Review Copilot code thoroughly
- Pair program when learning

### Prevention
- Pair programming sessions
- Manual code reviews
- Regular training
- Measure code quality metrics

---

## Pitfall 5: Inconsistent Style

### ❌ The Problem
```javascript
// Developer A's code
const getData = () => {
  return fetch('/api/data').then(r => r.json());
}

// Developer B's Copilot code
async function getData() {
  const response = await fetch('/api/data');
  return response.json();
}

// Different style, confuses team
```

### ✅ The Solution
```javascript
// Establish style guide in CLAUDE.md
// All developers follow same style
const getData = async () => {
  const response = await fetch('/api/data');
  return response.json();
};
```

### Prevention
- Create CLAUDE.md with style guide
- Use ESLint/Prettier enforced
- Establish patterns first
- Code review for consistency

---

## Pitfall 6: Incomplete Testing

### ❌ The Problem
```javascript
// Copilot generates code
function calculateDiscount(price, discountRate) {
  return price * (1 - discountRate);
}

// Developer doesn't test edge cases
// Fails with negative price or rate > 1
```

### ✅ The Solution
```javascript
function calculateDiscount(price, discountRate) {
  // Validate inputs
  if (price < 0 || discountRate < 0 || discountRate > 1) {
    throw new Error('Invalid input');
  }
  return price * (1 - discountRate);
}

// Test edge cases
test('handles edge cases', () => {
  expect(() => calculateDiscount(-1, 0.1)).toThrow();
  expect(() => calculateDiscount(100, 1.5)).toThrow();
});
```

### Prevention
- Write tests before Copilot generates
- Test edge cases
- Test error conditions
- Test performance (if critical)

---

## Pitfall 7: Complex Code in One Function

### ❌ The Problem
```javascript
// Huge function that tries to do everything
function processOrder(order) {
  // 200 lines of code
  // Copilot struggles with context
  // Output is poor quality
}
```

### ✅ The Solution
```javascript
// Break into smaller functions
function validateOrder(order) { }
function calculateTotal(order) { }
function processPayment(order) { }
function updateInventory(order) { }
function notifyCustomer(order) { }

// Copilot excels at smaller functions
```

### Prevention
- Keep functions small (< 30 lines)
- Single responsibility principle
- Break complex logic into steps
- Compose from smaller functions

---

## Pitfall 8: Ignoring Performance

### ❌ The Problem
```javascript
// Copilot suggests naive O(n²) solution
function removeDuplicates(array) {
  return array.filter((item, index) =>
    array.indexOf(item) === index  // O(n²) operation!
  );
}

// Works fine for small arrays, fails at scale
```

### ✅ The Solution
```javascript
// More efficient O(n) solution
function removeDuplicates(array) {
  return [...new Set(array)];  // O(n) operation
}

// Or more readable
function removeDuplicates(array) {
  const seen = new Set();
  return array.filter(item => {
    if (seen.has(item)) return false;
    seen.add(item);
    return true;
  });
}
```

### Prevention
- Consider algorithm complexity
- Test with realistic data sizes
- Profile performance
- Ask for specific approach: "use Set for O(n) performance"

---

## Pitfall 9: Not Committing to Version Control

### ❌ The Problem
```bash
# Lots of uncommitted Copilot code
# If something breaks, hard to debug
# Can't revert to working state
```

### ✅ The Solution
```bash
# Commit frequently
git add .
git commit -m "feat: add user validation

- Add validateEmail function
- Add password strength check
- Add test coverage"

# Create PR for review
# Merge after approval
```

### Prevention
- Commit after each small feature
- Use meaningful commit messages
- Create PRs for review
- Use git hooks to enforce quality

---

## Pitfall 10: Not Updating Documentation

### ❌ The Problem
```javascript
// Copilot generates new function
function calculateComplexFormula(x, y, z) {
  // No comment explaining what this does
  return (x * y) / (z + 1);
}

// Six months later, nobody remembers
```

### ✅ The Solution
```javascript
/**
 * Calculate efficiency score based on three factors
 * @param productivityScore - Efficiency measure (0-100)
 * @param qualityScore - Output quality (0-100)
 * @param timeInvested - Time spent (hours)
 * @returns Efficiency metric
 * 
 * Formula: (productivity * quality) / (time + 1)
 */
function calculateComplexFormula(
  productivityScore,
  qualityScore,
  timeInvested
) {
  return (productivityScore * qualityScore) / (timeInvested + 1);
}
```

### Prevention
- Document functions with JSDoc/docstrings
- Explain "why" in comments
- Update README when adding features
- Keep architectural docs current

---

## Pitfall Checklist

Before committing Copilot-generated code:

- [ ] Code reviewed (not blindly accepted)
- [ ] Proper context provided (not vague)
- [ ] No security issues
- [ ] Tests written and passing
- [ ] Style consistent with project
- [ ] Performance adequate
- [ ] Documentation updated
- [ ] Committed to version control

---

**Previous**: [Team Standards](./02-team-standards.md)  
**Next**: [Security & Compliance](./05-security-compliance.md)
