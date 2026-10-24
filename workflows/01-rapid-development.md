# Rapid Development Workflow with GitHub Copilot

## Overview

The **Rapid Development Workflow** maximizes Copilot's code generation to build features quickly while maintaining quality.

## The Workflow

```
Plan → Structure → Generate → Test → Review → Commit
  ↓         ↓         ↓        ↓       ↓        ↓
10min   15min    20min     15min   10min    5min
```

## Phase 1: Plan (10 minutes)

### Step 1: Define Requirements

```markdown
# Feature: User Authentication

## Requirements
- User login with email/password
- JWT token generation
- Token validation
- Logout functionality

## Acceptance Criteria
- [ ] User can log in with valid credentials
- [ ] User receives JWT token
- [ ] Invalid credentials rejected
- [ ] Token expires after 24 hours
```

### Step 2: Break Into Tasks

```javascript
// Tasks to implement
[
  "Create User model with email/password fields",
  "Create login endpoint",
  "Create token generation function",
  "Create token validation middleware",
  "Create logout endpoint",
  "Write tests for auth flow"
]
```

## Phase 2: Structure (15 minutes)

### Create File Structure

```bash
src/
├── models/
│   └── User.ts
├── services/
│   ├── AuthService.ts
│   └── TokenService.ts
├── controllers/
│   └── AuthController.ts
├── middleware/
│   └── authMiddleware.ts
└── types/
    └── index.ts
```

### Create Type Definitions

```typescript
// src/types/index.ts

interface User {
  id: string;
  email: string;
  password: string;  // hashed
  createdAt: Date;
}

interface LoginRequest {
  email: string;
  password: string;
}

interface LoginResponse {
  token: string;
  user: Omit<User, 'password'>;
}

interface TokenPayload {
  userId: string;
  email: string;
  iat: number;
  exp: number;
}
```

## Phase 3: Generate (20 minutes)

### Copilot-Powered Generation

#### Step 1: Generate Models

```typescript
// src/models/User.ts

import mongoose, { Schema, Document } from 'mongoose';

interface UserDoc extends Document {
  email: string;
  password: string;
}

// Copilot will suggest the schema
const userSchema = new Schema<UserDoc>({
  
});

export const User = mongoose.model<UserDoc>('User', userSchema);
```

#### Step 2: Generate Services

```typescript
// src/services/AuthService.ts

import bcrypt from 'bcrypt';
import { User } from '../models/User';
import { LoginRequest, LoginResponse } from '../types';

export class AuthService {
  // Login user and return JWT token
  async login(credentials: LoginRequest): Promise<LoginResponse> {
    
  }

  // Logout user (invalidate token)
  async logout(userId: string): Promise<void> {
    
  }
}
```

#### Step 3: Generate Controllers

```typescript
// src/controllers/AuthController.ts

import { Request, Response } from 'express';
import { AuthService } from '../services/AuthService';

export class AuthController {
  private authService = new AuthService();

  // Handle login request
  async login(req: Request, res: Response): Promise<void> {
    
  }

  // Handle logout request
  async logout(req: Request, res: Response): Promise<void> {
    
  }
}
```

#### Step 4: Generate Middleware

```typescript
// src/middleware/authMiddleware.ts

import { Request, Response, NextFunction } from 'express';

// Verify JWT token and attach user to request
export function authMiddleware(
  req: Request,
  res: Response,
  next: NextFunction
): void {
  
}
```

#### Step 5: Generate Routes

```typescript
// src/routes/auth.ts

import express from 'express';
import { AuthController } from '../controllers/AuthController';
import { authMiddleware } from '../middleware/authMiddleware';

const router = express.Router();
const authController = new AuthController();

// POST /auth/login
router.post('/login', (req, res) => authController.login(req, res));

// POST /auth/logout - requires authentication
router.post('/logout', authMiddleware, (req, res) => 
  authController.logout(req, res)
);

export default router;
```

## Phase 4: Test (15 minutes)

### Generate Tests

```typescript
// tests/auth.test.ts

describe('Authentication', () => {
  describe('login', () => {
    test('returns token for valid credentials', async () => {
      // Copilot suggests test implementation
      
    });

    test('throws error for invalid credentials', async () => {
      // Copilot suggests error handling test
      
    });
  });

  describe('logout', () => {
    test('invalidates user token', async () => {
      // Copilot suggests logout test
      
    });
  });
});
```

### Run Tests

```bash
npm test -- --watch
```

## Phase 5: Review (10 minutes)

### Code Review Checklist

```javascript
[
  "✓ All tests passing",
  "✓ No TypeScript errors",
  "✓ Proper error handling",
  "✓ No hardcoded secrets",
  "✓ Input validation present",
  "✓ Code follows project style",
  "✓ Comments are clear",
  "✓ No console.log in production"
]
```

### Manual Testing

```bash
# Start dev server
npm run dev

# Test login
curl -X POST http://localhost:3000/auth/login \
  -H "Content-Type: application/json" \
  -d '{"email":"user@example.com","password":"password123"}'

# Test with token
curl http://localhost:3000/protected \
  -H "Authorization: Bearer <token>"
```

## Phase 6: Commit (5 minutes)

```bash
# Stage changes
git add -A

# Commit with descriptive message
git commit -m "feat: add JWT authentication

- Implement user login with email/password
- Generate and validate JWT tokens
- Add authentication middleware
- Add token expiration and refresh logic
- Add comprehensive test suite"

# Push to branch
git push origin feature/auth
```

## Copilot Tips for Rapid Development

### Tip 1: Establish Patterns First

```typescript
// Establish pattern in first file
async function validateUser(user: User): Promise<boolean> {
  // Validate structure
}

// Copilot copies pattern in subsequent files
async function validateRequest(req: Request): Promise<boolean> {
  // Copilot suggests similar pattern
}
```

### Tip 2: Use Descriptive Names

```typescript
// ✅ Good - Copilot understands intent
async function hashPasswordAndSave(user: User): Promise<void> { }

// ❌ Vague - Copilot guesses
async function process(data: any): Promise<void> { }
```

### Tip 3: Keep Files Focused

```typescript
// ✅ Focused file
// AuthController.ts - only auth logic

// ❌ Mixed concerns
// Controller.ts - auth + users + posts (too much)
```

### Tip 4: Use Open Files for Context

```
Tab 1: User.ts (model definition)
Tab 2: AuthService.ts (currently editing)
Tab 3: types/index.ts (type definitions)

Copilot uses all three for better context
```

## Rapid Development Checklist

- [ ] Requirements documented
- [ ] File structure created
- [ ] Types defined
- [ ] Services implemented (Copilot-generated)
- [ ] Controllers implemented (Copilot-generated)
- [ ] Routes created (Copilot-generated)
- [ ] Tests written (Copilot-generated)
- [ ] All tests passing
- [ ] Code reviewed
- [ ] Changes committed

## Time Breakdown Example

| Phase | Task | Time | Copilot% |
|-------|------|------|----------|
| Plan | Requirements | 10 min | 0% |
| Structure | File setup | 15 min | 10% |
| Generate | Services | 20 min | 80% |
| Test | Write tests | 15 min | 60% |
| Review | Manual check | 10 min | 0% |
| Commit | Git workflow | 5 min | 0% |
| **Total** | | **75 min** | **38%** |

## Scaling the Workflow

### For Larger Features

- Break into smaller, releasable pieces
- Implement one piece using this workflow
- Deploy piece
- Move to next piece

### For Team Collaboration

- One developer per feature
- Code review before merge
- Establish shared patterns document
- Use CLAUDE.md for consistency

## Common Mistakes to Avoid

1. **Skipping tests** — Always test Copilot-generated code
2. **Not reviewing** — Review before committing
3. **Accepting blindly** — Check every suggestion
4. **Poor naming** — Helps Copilot and humans
5. **Huge files** — Keep focused scope

---

**Next**: [Test-Driven Development Workflow](./02-tdd-workflow.md)
