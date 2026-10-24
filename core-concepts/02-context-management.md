# Context Management in GitHub Copilot

## What is Context?

**Context** = Information Copilot uses to generate suggestions

### Types of Context

```
Current File Context
├── Entire current file (code structure)
├── Current cursor position
├── Surrounding functions/classes
└── Recent edits

Project Context
├── File structure
├── Language type
├── Similar files
└── .copilotignore patterns

Environmental Context
├── Open files in editor
├── Git history
├── Dependencies
└── Configuration files
```

## Managing Effective Context

### Principle 1: Proximity Matters

Copilot reads **before and after** your cursor:

```javascript
// Copilot uses all of this context

class UserService {
  constructor(db) {
    this.db = db;
  }

  // ← Cursor here
  // Copilot understands UserService structure
  // and generates appropriate methods
}
```

### Principle 2: Clear Code Structure

Good structure = Better suggestions:

```javascript
// ✅ GOOD - Clear structure
class PaymentProcessor {
  processPayment(amount, currency) {
    // Copilot understands the method purpose
  }

  refundPayment(transactionId) {
    // Clear method names help
  }
}

// ❌ POOR - Unclear structure
class Payment {
  p(a, c) {  // Vague naming
    // Copilot confused about intent
  }
}
```

### Principle 3: Intentional Comments

Comments focus context:

```javascript
// ❌ Without comment
function validateUser(user) {
  
}

// ✅ With comment - Better suggestions
function validateUser(user) {
  // Check if user has required fields: email, password, name
  
}

// ✅✅ Even better - Specific format
function validateUser(user) {
  // Validate user object has:
  // - email: valid email format
  // - password: min 8 characters
  // - name: non-empty string
  // Return {valid: boolean, errors: string[]}
  
}
```

## Context Optimization Techniques

### 1. Open Relevant Files

Keep related files open:
- Model definitions
- API specs
- Similar implementations
- Type definitions

```
Open Tabs Strategy:
├── user.model.ts (current)
├── user.service.ts (related)
├── user.controller.ts (context)
└── types.ts (definitions)
```

### 2. Structure Your Code

Bad structure hurts Copilot:

```javascript
// ❌ Everything crammed together
function api() { ... }
function db() { ... }
class X { ... }

// ✅ Clear organization
// Controllers
class UserController { ... }

// Services
class UserService { ... }

// Models
class User { ... }
```

### 3. Use Type Definitions

Types provide crucial context:

```typescript
// ❌ No types - Copilot guessing
function getUser(id) {
  // What's the return type?
}

// ✅ With types - Clear context
interface User {
  id: number;
  email: string;
  name: string;
}

function getUser(id: number): Promise<User> {
  // Copilot knows exact requirements
}
```

### 4. Name Things Well

Naming = Context:

```javascript
// ❌ Poor naming
function proc(x, y) {
  // What does this do?
}

// ✅ Clear naming
function calculateMonthlyInvoiceTotal(invoice, taxRate) {
  // Purpose is obvious
}
```

### 5. Establish Patterns

Patterns help Copilot predict:

```javascript
// Establish pattern
async function fetchUsers() {
  const response = await fetch('/api/users');
  const data = await response.json();
  return data;
}

// Now Copilot knows the pattern
async function fetchPosts() {
  // Copilot suggests similar implementation
  
}
```

## Context Anti-Patterns to Avoid

### Too Much Context
```javascript
// ❌ Huge function - Copilot loses focus
function processOrder(order) {
  // 200 lines of code
  // Context window gets full
  // Suggestions become poor
}

// ✅ Break into smaller functions
function validateOrder(order) { }
function calculateOrderTotal(order) { }
function processPayment(order) { }
```

### Missing Context
```javascript
// ❌ No context
function x() {
  
}

// ✅ Provide context
function calculateUserAgeInMonths() {
  // Given a user's birth date, calculate current age in months
  
}
```

### Conflicting Context
```javascript
// ❌ Conflicting naming
class User {
  getName() { return this.surname; }  // Confusing!
}

// ✅ Consistent
class User {
  getFullName() { return this.firstName + ' ' + this.lastName; }
}
```

## Context for Different File Types

### JavaScript/TypeScript
```javascript
// Helpful context
import { User } from './types';
import { validateEmail } from './utils';

class UserService {
  async getUser(id: number): Promise<User> {
    // Implementation
  }
}
```

### Python
```python
from typing import List, Optional
from models import User
from utils import validate_email

class UserService:
    def get_user(self, user_id: int) -> Optional[User]:
        """Retrieve user by ID."""
        # Implementation
```

### Java
```java
import java.util.Optional;
import com.example.models.User;
import com.example.utils.Validation;

public class UserService {
    public Optional<User> getUser(int userId) {
        // Implementation
    }
}
```

## Project-Level Context

### .copilotignore Strategy

```
# Exclude to reduce noise
*.generated.ts
*.min.js
coverage/
dist/
node_modules/

# Keep strategic context
src/
tests/
```

### CLAUDE.md Context

Create project guide:

```markdown
# Project Structure
- src/models/ — Data models
- src/services/ — Business logic
- src/controllers/ — API handlers

# Code Style
- TypeScript with strict mode
- Functional components preferred
- Use async/await, no callbacks
```

## Advanced: Token Context Window

### Understanding Tokens

```
1 Token ≈ 4 characters (rough estimate)

Context Window: ~3,000 tokens
            ≈ 12,000 characters
            ≈ 150-200 lines of code
```

### Optimization for Large Files

```javascript
// In large file: only recent context used

// ↑ Old code (not in context window)
// 
// ✓ Recent code (in context window)
// ← Cursor position
// ✓ Next code (in context window)
// 
// ↓ Future code (not in context window)
```

## Context Checklist

Before requesting Copilot suggestions:

- [ ] Clear file structure
- [ ] Relevant files open
- [ ] Type definitions provided
- [ ] Function names descriptive
- [ ] Pattern established
- [ ] Comments clear and specific
- [ ] Related code nearby
- [ ] No conflicting patterns

## Key Takeaways

1. **Context is Everything** — Better context = better suggestions
2. **Proximity Matters** — Nearby code influences suggestions
3. **Naming is Communication** — Good names = better understanding
4. **Types Help** — Type definitions provide crucial context
5. **Keep It Clean** — Remove noise from context

---

**Previous**: [How Copilot Works](./01-how-copilot-works.md)  
**Next**: [Prompting Techniques](./03-prompting-techniques.md)
