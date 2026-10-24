# Language-Specific Guides

## Supported Languages

### Tier 1 (Excellent Support)

- [JavaScript](#javascript) — Most common, excellent support
- [Python](#python) — Data science & backend
- [TypeScript](#typescript) — Type-safe JavaScript
- [Java](#java) — Enterprise backend
- [C#](#csharp) — .NET ecosystem
- [Go](#go) — Systems programming
- [Ruby](#ruby) — Web development

### Tier 2 (Good Support)

- [Rust](#rust) — Systems programming
- [Kotlin](#kotlin) — JVM alternative
- [Bash/Shell](#bashshell) — Scripting
- [PHP](#php) — Web development

### Tier 3 (Basic Support)

- [Scala, Clojure, Haskell, Elixir, etc.](#tier-3-languages)

---

## JavaScript

### Best Prompting

```javascript
// Clear comment
// Convert array of objects to map with id as key
function arrayToMap(items) {
  
}

// Copilot output
function arrayToMap(items) {
  return items.reduce((map, item) => {
    map[item.id] = item;
    return map;
  }, {});
}
```

### Copilot Strength: **Very Good**
- Excellent for ES6+ syntax
- Strong async/await support
- Good with common libraries (lodash, moment, etc.)

---

## Python

### Best Prompting

```python
# Clear comment with type hints
def validate_email(email: str) -> bool:
    # Check if email contains @ and .
    # Return True if valid, False otherwise
    pass

# Copilot output
def validate_email(email: str) -> bool:
    return '@' in email and '.' in email.split('@')[1]
```

### Copilot Strength: **Very Good**
- Excellent type hint support
- Strong with standard library
- Good with pandas, numpy patterns

---

## TypeScript

### Best Prompting

```typescript
interface User {
  id: number;
  email: string;
  name: string;
}

// Function to find user by email
function findUserByEmail(users: User[], email: string): User | undefined {
  
}

// Copilot output
function findUserByEmail(users: User[], email: string): User | undefined {
  return users.find(user => user.email === email);
}
```

### Copilot Strength: **Excellent**
- Strong with interfaces
- Excellent type inference
- Good with React patterns

---

## Java

### Best Prompting

```java
// Convert list of users to map with id as key
public static Map<Integer, User> usersToMap(List<User> users) {
  
}

// Copilot output
public static Map<Integer, User> usersToMap(List<User> users) {
  return users.stream()
    .collect(Collectors.toMap(User::getId, Function.identity()));
}
```

### Copilot Strength: **Very Good**
- Good with streams API
- Strong with Spring patterns
- Excellent with common libraries

---

## Go

### Best Prompting

```go
// Validate email address
func ValidateEmail(email string) bool {
  
}

// Copilot output
func ValidateEmail(email string) bool {
  return strings.Contains(email, "@") && strings.Contains(email, ".")
}
```

### Copilot Strength: **Good**
- Strong with goroutine patterns
- Good with standard library
- Decent with common frameworks

---

## Ruby

### Best Prompting

```ruby
# Convert array of hashes to hash with id as key
def array_to_hash(items)
  
end

# Copilot output
def array_to_hash(items)
  items.reduce({}) { |hash, item| hash[item[:id]] = item; hash }
end
```

### Copilot Strength: **Good**
- Good with Ruby idioms
- Strong with Rails patterns
- Decent with common gems

---

## C#

### Best Prompting

```csharp
// Convert list of users to dictionary with id as key
public Dictionary<int, User> UsersToDictionary(List<User> users) {
  
}

// Copilot output
public Dictionary<int, User> UsersToDictionary(List<User> users) {
  return users.ToDictionary(u => u.Id, u => u);
}
```

### Copilot Strength: **Very Good**
- Excellent LINQ support
- Strong with .NET ecosystem
- Good with async/await

---

## Rust

### Best Prompting

```rust
// Convert vector of users to hashmap with id as key
fn users_to_map(users: Vec<User>) -> HashMap<u32, User> {
  
}

// Copilot output
fn users_to_map(users: Vec<User>) -> HashMap<u32, User> {
  users.into_iter().map(|u| (u.id, u)).collect()
}
```

### Copilot Strength: **Good**
- Good with ownership patterns
- Decent with macros
- Strong with common crates

---

## Bash/Shell

### Best Prompting

```bash
#!/bin/bash

# Count lines in all .ts files in src directory
count_lines() {
  
}

# Copilot output
count_lines() {
  find src -name "*.ts" -type f -exec wc -l {} + | tail -1
}
```

### Copilot Strength: **Good**
- Good with common shell patterns
- Decent with pipes and redirects
- Strong with file operations

---

## Tier 3 Languages

For languages with basic Copilot support:

1. **Use standard patterns** — Establish clear patterns
2. **Be very specific** — Comments must be detailed
3. **Show examples** — Comments with examples help
4. **Keep it simple** — Complex logic needs extra guidance
5. **Review carefully** — Always thoroughly test output

### Example (Scala)

```scala
// Convert list of users to map with id as key
def usersToMap(users: List[User]): Map[Int, User] = {
  
}
```

---

## Cross-Language Tips

### ✅ DO

- Use language idioms (not just pseudocode)
- Provide type information
- Show established patterns
- Use language-standard libraries
- Comment clearly in that language

### ❌ DON'T

- Mix languages in comments
- Use pseudocode
- Ignore language conventions
- Use outdated syntax
- Expect patterns Copilot doesn't know

---

**Go back**: [Recipes](./README.md)
