# Code Generation Patterns with GitHub Copilot

## Understanding Generation Patterns

**Pattern**: A reusable template for code generation that Copilot recognizes and can reliably generate.

## Core Patterns

### Pattern 1: CRUD Operations

```javascript
// CREATE
function createUser(userData) {
  // Copilot generates insert/save logic
}

// READ
function getUser(userId) {
  // Copilot generates fetch/select logic
}

// UPDATE
function updateUser(userId, userData) {
  // Copilot generates update logic
}

// DELETE
function deleteUser(userId) {
  // Copilot generates delete logic
}
```

### Pattern 2: Validation Pattern

```javascript
// Standard validation structure
function validateEmail(email) {
  // Check if email includes @ symbol
  // Check if email includes . after @
  // Return true if valid, false otherwise
}

function validatePassword(password) {
  // Check if password is at least 8 characters
  // Check if password includes uppercase letter
  // Check if password includes number
  // Return true if valid, false otherwise
}
```

### Pattern 3: Error Handling

```javascript
try {
  // Attempt operation
  const result = riskyOperation();
  return result;
} catch (error) {
  // Handle error
  console.error('Operation failed:', error.message);
  throw error;
}
```

### Pattern 4: Array Transformation

```javascript
// Map: Transform each element
const doubled = numbers.map(n => n * 2);

// Filter: Keep matching elements
const evens = numbers.filter(n => n % 2 === 0);

// Reduce: Combine into single value
const sum = numbers.reduce((acc, n) => acc + n, 0);

// Find: Get first match
const firstEven = numbers.find(n => n % 2 === 0);
```

### Pattern 5: Async/Await

```javascript
async function fetchAndProcess(url) {
  try {
    const response = await fetch(url);
    const data = await response.json();
    return processData(data);
  } catch (error) {
    console.error('Fetch failed:', error);
    throw error;
  }
}
```

## Language-Specific Patterns

### TypeScript Interface Pattern

```typescript
// Copilot generates properties based on interface name
interface User {
  id: number;
  email: string;
  name: string;
}

// Copilot knows User structure for type-safe code
function processUser(user: User): void {
  
}
```

### Python Dataclass Pattern

```python
from dataclasses import dataclass

@dataclass
class User:
    id: int
    email: str
    name: str
```

### Java Class Pattern

```java
public class User {
    private int id;
    private String email;
    private String name;
    
    // Copilot generates getters/setters
    public int getId() {
        
    }
}
```

## API Endpoint Patterns

### REST GET Endpoint

```javascript
// GET endpoint that returns a list
app.get('/users', (req, res) => {
  // Copilot generates: fetch data, return JSON
  
});

// GET endpoint with ID
app.get('/users/:id', (req, res) => {
  // Copilot generates: fetch by ID, return single item
  
});
```

### REST POST Endpoint

```javascript
// Create new resource
app.post('/users', (req, res) => {
  // Copilot generates: validate, save, return created item
  
});
```

### REST PUT/PATCH Endpoint

```javascript
// Update resource
app.put('/users/:id', (req, res) => {
  // Copilot generates: validate, update, return modified item
  
});
```

### REST DELETE Endpoint

```javascript
// Delete resource
app.delete('/users/:id', (req, res) => {
  // Copilot generates: delete, return success response
  
});
```

## Test Patterns

### Unit Test Pattern

```javascript
describe('validateEmail', () => {
  test('returns true for valid email', () => {
    // Copilot generates assertion
    expect(validateEmail('test@example.com')).toBe(true);
  });
  
  test('returns false for invalid email', () => {
    // Copilot generates assertion
    expect(validateEmail('invalid')).toBe(false);
  });
});
```

### Integration Test Pattern

```javascript
describe('User API', () => {
  test('POST /users creates a new user', async () => {
    // Copilot generates: request, assertion
    
  });
});
```

## Component Patterns

### React Component

```javascript
function UserProfile({ userId }) {
  const [user, setUser] = useState(null);
  
  useEffect(() => {
    // Copilot generates fetch logic
    
  }, [userId]);
  
  return (
    // Copilot generates JSX
    <div></div>
  );
}
```

### Vue Component

```javascript
export default {
  props: ['userId'],
  data() {
    return {
      // Copilot generates data properties
      user: null
    };
  },
  mounted() {
    // Copilot generates initialization
    
  }
}
```

## Hook Patterns

### Middleware/Decorator

```javascript
// Express middleware
function authMiddleware(req, res, next) {
  // Copilot generates: token check, authorization
  
}

// Usage
app.use(authMiddleware);
```

### Custom Hook (React)

```javascript
function useUser(userId) {
  const [user, setUser] = useState(null);
  const [loading, setLoading] = useState(true);
  
  useEffect(() => {
    // Copilot generates fetch logic
    
  }, [userId]);
  
  return { user, loading };
}
```

## Configuration Patterns

### Environment Config

```javascript
// Copilot recognizes this pattern
const config = {
  apiUrl: process.env.API_URL || 'http://localhost:3000',
  dbUrl: process.env.DB_URL || 'mongodb://localhost',
  port: process.env.PORT || 3000
};
```

### Feature Flags

```javascript
const features = {
  newUserUI: true,
  betaAPI: false,
  darkMode: process.env.DARK_MODE === 'true'
};
```

## Data Structure Patterns

### Nested Object

```javascript
const userData = {
  id: 1,
  profile: {
    name: 'John',
    email: 'john@example.com'
  },
  settings: {
    notifications: true,
    theme: 'dark'
  }
};
```

### Array of Objects

```javascript
const users = [
  { id: 1, name: 'John', email: 'john@example.com' },
  { id: 2, name: 'Jane', email: 'jane@example.com' },
  { id: 3, name: 'Bob', email: 'bob@example.com' }
];
```

## How to Leverage Patterns

### 1. Recognize the Pattern
When you start typing, think: "Is this a common pattern Copilot knows?"

### 2. Start the Pattern
Begin with the pattern structure:
```javascript
function validateEmail(email) {
  // Copilot recognizes "validate" pattern
}
```

### 3. Let Copilot Complete
Type the comment, Copilot suggests the implementation

### 4. Review & Adjust
Check if suggestion matches your pattern, adjust if needed

## Anti-Patterns to Avoid

### ❌ Non-Standard Patterns

```javascript
// Copilot struggles with non-standard approaches
function weirdValidation(x) {
  // Unusual logic that breaks patterns
}
```

**Solution**: Use standard patterns that Copilot understands

### ❌ Mixed Patterns

```javascript
// Don't mix multiple patterns
function doEverything() {
  // Fetch data
  // Validate data
  // Transform data
  // Save data
  // Return result
}
```

**Solution**: Separate into single-responsibility functions

## Pattern Composition

### Building Complex Logic from Patterns

```javascript
// Combine multiple patterns

// Pattern 1: Fetch
async function fetchUsers() { }

// Pattern 2: Validate
function validateUser(user) { }

// Pattern 3: Transform
function transformUser(user) { }

// Pattern 4: Compose
async function processUsers() {
  const users = await fetchUsers();  // Pattern 1
  return users
    .filter(u => validateUser(u))    // Pattern 2
    .map(u => transformUser(u));     // Pattern 3
}
```

## Key Takeaways

1. **Patterns Are Powerful** — Copilot recognizes standard patterns
2. **Use Standard Names** — `getUser`, `validateEmail` help Copilot
3. **Structure Matters** — Clean structure enables pattern recognition
4. **Type Hints** — Types make patterns explicit
5. **Combine Patterns** — Build complex logic from simple patterns

---

**Previous**: [Prompting Techniques](./03-prompting-techniques.md)  
**Next**: [Rapid Development Workflow](../workflows/01-rapid-development.md)
