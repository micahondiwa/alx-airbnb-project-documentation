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

**Security:**

- Passwords hashed using bcrypt

- JWT tokens expire in 24 hours

- Rate limiting (e.g., 5 attempts per IP per hour)

**Performance:**

- Authentication response under 300ms

## 2. Property Management

**Objective:**

Allow hosts to add, edit, delete, and retrieve property listings.

API Endpoints:

- POST /api/properties/

    Create a new property listing.

    Input (Multipart Form):
     - title (string, required)
     - description (string)
     - price_per_night (float, required)
     - location (string, required)
     - amenities (array of strings)
     - images[] (files)

```json
{
  "id": "property_id",
  "title": "...",
  "host_id": "user_id",
  ...
}
```
- PUT /api/properties/:id

Edit a property listing.

- DELETE /api/properties/:id

Remove a property.

- GET /api/properties/?location=&price_min=&price_max=...
Search listings with filters.

**Validation Rules:**
- Only hosts can create/edit/delete
- Title max 100 characters
- Price must be > 0

**Storage:**
- Images stored in AWS S3 or Cloudinary
- Metadata in PostgreSQL

**Performance:**
- Listing fetch time under 500ms with filters
- Pagination enabled (20 per page)

## 3. Booking System

**Objective:**

Enable guests to book available properties and manage bookings.

**API Endpoints:**

- POST /api/bookings/
    Create a booking.

```json
{
  "property_id": "abc123",
  "start_date": "2025-07-15",
  "end_date": "2025-07-20"
}

{
  "booking_id": "...",
  "status": "pending",
  "total_price": 500
}

```

