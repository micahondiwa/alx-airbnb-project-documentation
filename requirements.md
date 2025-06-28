# Backend Feature Requirement Specifications – Airbnb Clone

This document outlines the functional and technical requirements for three key backend features of the Airbnb Clone project:

- User Authentication
- Property Management
- Booking System

---

## 1. User Authentication

### Objective:
Allow users to register, log in, and manage authentication securely.

### API Endpoints:

- **POST /api/auth/register**  
  Registers a new user.

  **Input (JSON):**

  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "StrongP@ss123",
    "role": "host"
  }
  ```

**Validation Rules:**

- Email must be valid and unique

- Password minimum 8 characters, include letters, numbers, and special characters

- Role must be either "guest" or "host"

```json
{
  "token": "jwt-token",
  "user": {
    "id": "user_id",
    "name": "John Doe",
    "email": "john@example.com",
    "role": "host"
  }
}
```

**POST /api/auth/login**
Authenticates existing user and returns a JWT.

```json
{
  "email": "john@example.com",
  "password": "StrongP@ss123"
}

{
  "token": "jwt-token",
  "user": { "id": "...", "name": "John Doe", "role": "host" }
}

```

