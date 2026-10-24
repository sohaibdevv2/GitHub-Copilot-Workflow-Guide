# Prompting Techniques for GitHub Copilot

## The Fundamentals

### What Makes a Good Prompt?

A good Copilot prompt has:

| Element | Example |
|---------|---------|
| **Clear intent** | What you want to accomplish |
| **Context** | Relevant information |
| **Specification** | Expected behavior/format |
| **Constraints** | Limitations or requirements |

## Prompting Patterns

### Pattern 1: The Descriptor Comment

```javascript
// Most common pattern

// Generate a function that validates email addresses
function validateEmail(email) {
  
}
```

**Works best for**: Functions, methods, implementations

### Pattern 2: The Specification Comment

```javascript
// More detailed pattern

// Parse a CSV string into an array of objects
// Input: "name,age,email\nJohn,30,john@example.com"
// Output: [{name: "John", age: "30", email: "john@example.com"}]
function parseCSV(csvString) {
  
}
```

**Works best for**: Complex logic, specific requirements

### Pattern 3: The Example Comment

```javascript
// Show by example

// Create a function that multiplies numbers
// Example: multiply(3, 4) returns 12
// Example: multiply(0, 5) returns 0
function multiply(a, b) {
  
}
```

**Works best for**: Edge cases, specific behaviors

### Pattern 4: The Task List Comment

```javascript
// Break down the task

// Sort an array and remove duplicates
// 1. Create a Set from the array (removes duplicates)
// 2. Convert Set back to array
// 3. Sort the array
// 4. Return sorted array
function sortUnique(arr) {
  
}
```

**Works best for**: Multi-step algorithms

### Pattern 5: The Format Specification

```javascript
// Specify the output format

// Convert timestamp to readable date string
// Format: "June 8, 2026 at 10:30 AM"
function formatDate(timestamp) {
  
}
```

**Works best for**: Formatting, parsing

## Prompting Techniques: Pro Tips

### 1. Be Specific

```javascript
// ❌ Vague
// Calculate total

// ✅ Specific
// Calculate total cost by summing prices and adding tax
function calculateTotalCost(items, taxRate) {
  
}
```

### 2. Use Existing Code as Context

```javascript
// ❌ Copilot confused
interface User {
  id: number;
  name: string;
}

function processUser(user) {
  // Copilot doesn't know what "process" means
}

// ✅ Copilot understands
interface User {
  id: number;
  name: string;
  email: string;
}

function validateUserEmail(user) {
  // Copilot knows User structure and purpose
  
}
```

### 3. Show Required Return Type

```typescript
// ❌ Return type unclear
function getUser(id: number) {
  
}

// ✅ Clear return type
function getUser(id: number): Promise<User> {
  
}

// Or as comment
// Returns: {id: number, name: string, email: string}
```

### 4. Reference Existing Patterns

```javascript
// Establish pattern first
function fetchUsers() {
  const response = await fetch('/api/users');
  return response.json();
}

// Then reference it
// Use same pattern as fetchUsers, but for posts
function fetchPosts() {
  
}
```

### 5. Use Variable Names as Hints

```javascript
// ❌ Generic names
function f(x, y) {
  
}

// ✅ Semantic names
function calculateMonthlyPayment(principalAmount, interestRate) {
  
}
```

## Common Prompting Scenarios

### Scenario 1: Generate a Function Body

```javascript
// Pattern: Descriptor comment + function signature

// Convert temperature from Celsius to Fahrenheit
function celsiusToFahrenheit(celsius) {
  
}
```

### Scenario 2: Generate Tests

```javascript
// Pattern: Test description

// Test that validateEmail returns true for valid emails
test('validateEmail returns true for valid emails', () => {
  
});
```

### Scenario 3: Generate Documentation

```typescript
/**
 * Calculate the factorial of a number
 * @param n - The number to calculate factorial for
 * @returns The factorial of n
 */
function factorial(n: number): number {
  
}
```

### Scenario 4: Generate a Class

```javascript
// Create a class that manages a shopping cart
class ShoppingCart {
  
}
```

### Scenario 5: Generate API Endpoints

```javascript
// Create a GET endpoint that returns all users
app.get('/users', (req, res) => {
  
});
```

### Scenario 6: Generate Database Queries

```python
# Get all active users with their orders, ordered by creation date
def get_active_users_with_orders():
    
```

## Advanced Prompting Strategies

### Strategy 1: Multi-Line Specification

```javascript
// Use multiple comments for complex requirements

// Function that calculates discount price
// Rules:
// - If purchase > $100: 10% discount
// - If purchase > $50: 5% discount
// - If purchase <= $50: no discount
// Return the discounted price (not the discount amount)
function calculateDiscountedPrice(purchaseAmount) {
  
}
```

### Strategy 2: Reference Implementation Pattern

```javascript
// Create an object transformer similar to mapUser but for Products
// Model after: const mapUser = (u) => ({ id: u.id, name: u.name })
function mapProduct(product) {
  
}
```

### Strategy 3: Error Handling Specification

```javascript
// Parse JSON and handle errors gracefully
// Return null if parsing fails, or the parsed object if success
function parseJSON(jsonString) {
  
}
```

### Strategy 4: Performance Hint

```javascript
// Efficiently get unique values from array without creating intermediate arrays
// Use Set for O(n) performance
function getUniqueValues(array) {
  
}
```

## Prompting Anti-Patterns

### ❌ Too Vague
```javascript
// Process the data
function processData(data) {
  
}
```
**Problem**: Copilot guesses at what you mean

### ❌ Too Complex
```javascript
// Build a distributed cache system with Redis, 
// Memcached fallback, with automatic invalidation,
// compression, and metrics collection
```
**Problem**: Break into smaller functions

### ❌ Conflicting Hints
```javascript
// Sum the array using map
// (map isn't used for summing - confusing!)
function sumArray(arr) {
  
}
```
**Problem**: Give clear, single intent

### ❌ Missing Context
```javascript
// Just write some code
function doStuff() {
  
}
```
**Problem**: Provide specific intent and requirements

## Prompting by Language

### JavaScript/TypeScript

```typescript
// Good TypeScript prompt
interface Product {
  id: number;
  name: string;
  price: number;
}

// Filter products by price range and sort by price ascending
function getProductsInPriceRange(
  products: Product[],
  minPrice: number,
  maxPrice: number
): Product[] {
  
}
```

### Python

```python
# Good Python prompt
from typing import List
from dataclasses import dataclass

@dataclass
class Product:
    id: int
    name: str
    price: float

# Filter products by price range and sort ascending
def get_products_in_price_range(
    products: List[Product],
    min_price: float,
    max_price: float
) -> List[Product]:
    """Return products within price range, sorted by price."""
```

### Java

```java
// Good Java prompt
public List<Product> getProductsInPriceRange(
    List<Product> products,
    BigDecimal minPrice,
    BigDecimal maxPrice) {
    // Filter by price range and sort by price ascending
    
}
```

## Iterating on Suggestions

### When the First Suggestion Isn't Right

```javascript
// ✗ First suggestion wasn't right, try alternative
// Use cycle suggestion: Alt+] or Alt+[

// If alternatives also don't work:
// Modify your prompt to be more specific

// ❌ Original (too vague)
// Sum the numbers

// ✅ Improved
// Sum positive numbers from the array, ignore negative
function sumPositive(numbers) {
  
}
```

## Prompting Checklist

Before hitting Tab:

- [ ] Comment clearly describes intent
- [ ] Function signature clear
- [ ] Parameter names semantic
- [ ] Return type specified (types/comment)
- [ ] Similar code patterns nearby
- [ ] Not asking for conflicting things
- [ ] Specific enough for good suggestion
- [ ] Not too complex for one step

## Key Principles

1. **Clarity** — Clear intent = better suggestions
2. **Specificity** — More detail = more accurate results
3. **Context** — Related code and patterns help
4. **Iteration** — Refine if suggestion isn't right
5. **Review** — Always check generated code

---

**Previous**: [Context Management](./02-context-management.md)  
**Next**: [Code Generation Patterns](./04-code-generation-patterns.md)
