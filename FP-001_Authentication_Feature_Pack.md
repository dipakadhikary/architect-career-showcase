
# FP-001 Authentication Feature Pack
Version: 1.0

## Objective

Provide secure authentication and authorization for the ACOS platform.

---

# Business Requirements

BR-AUTH-001
A user can register with email and password.

BR-AUTH-002
A registered user can log in securely.

BR-AUTH-003
The system issues JWT access and refresh tokens.

BR-AUTH-004
Authenticated users can view and update their profile.

---

# User Stories

AUTH-001 Register
AUTH-002 Login
AUTH-003 Refresh Token
AUTH-004 Logout
AUTH-005 View Profile
AUTH-006 Update Profile

---

# Domain Model

Aggregate Root
- User

Entities
- Role
- RefreshToken

Value Objects
- Email
- PasswordHash

---

# Database

users
- id (UUID)
- email
- password_hash
- first_name
- last_name
- enabled
- created_at
- updated_at
- version

roles
- id
- name

user_roles
- user_id
- role_id

refresh_tokens
- id
- user_id
- token
- expires_at
- revoked

---

# REST API

POST /api/v1/auth/register
POST /api/v1/auth/login
POST /api/v1/auth/refresh
POST /api/v1/auth/logout

GET /api/v1/users/me
PUT /api/v1/users/me

---

# Security

- Spring Security 6
- JWT Access Token (15 min)
- Refresh Token (7 days)
- BCrypt password hashing
- RBAC
- Stateless APIs

---

# Validation

Register
- Valid email
- Password >= 12 chars
- Upper/lowercase
- Number
- Special character

---

# Error Model

AUTH-001 EmailAlreadyExists
AUTH-002 InvalidCredentials
AUTH-003 TokenExpired
AUTH-004 TokenRevoked
AUTH-005 Unauthorized

---

# Backend Tasks

- User Entity
- Role Entity
- RefreshToken Entity
- UserRepository
- AuthService
- JwtService
- TokenService
- AuthController
- SecurityConfig
- GlobalExceptionHandler

---

# Frontend Tasks

- Login Page
- Register Page
- Profile Page
- Protected Route
- Auth Context
- Token Refresh Interceptor

---

# Testing

Unit
- AuthService
- JwtService

Integration
- Register
- Login
- Refresh

E2E
- Login -> Dashboard
- Logout

---

# Interview Discussion

Why JWT instead of Session?

Why Refresh Token?

Why Stateless?

How would you revoke tokens?

How would you support SSO later?

---

# Definition of Done

- All APIs implemented
- Swagger updated
- Tests pass
- Flyway migration complete
- Docker Compose works
- Architecture review completed
