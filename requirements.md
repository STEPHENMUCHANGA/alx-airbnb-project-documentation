## Backend Feature Requirement Specifications – Airbnb Clone

This document outlines the technical and functional requirements for three key backend features: **User Authentication**, **Property Management**, and **Booking System**.

---

### 1. User Authentication

#### Functional Requirements
- Users must be able to register and log in securely.
- Roles supported: `guest`, `host`, and `admin`.
- JWT tokens used for session management.
- OAuth support (optional).

#### API Endpoints

##### 1.1 Register User
- **POST** `/api/auth/register`
- **Input:**
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "role": "host",
  "first_name": "Jane",
  "last_name": "Doe"
}
--- Validation:

--- Email must be unique and valid.

--- Password must be at least 8 characters.

--- Role must be one of: guest, host, admin.

--- Output (Success):

json
Copy
Edit
{
  "message": "User registered successfully",
  "token": "JWT_TOKEN_HERE"
}
Output (Failure):

json
Copy
Edit
{
  "error": "Email already in use"
}

##### 1.2 Login User
POST /api/auth/login

Input:

json
Copy
Edit
{
  "email": "user@example.com",
  "password": "securePassword123"
}
Output (Success):

json
Copy
Edit
{
  "token": "JWT_TOKEN_HERE",
  "user": {
    "id": "uuid",
    "role": "guest"
  }
}

Property Management
Functional Requirements
Hosts can create, update, or delete their property listings.

Guests can view and filter listings.

Listings include title, description, price, location, amenities, images.

## API Endpoints
### 2.1 Create Property
POST /api/properties

Input:

json
Copy
Edit
{
  "name": "Modern Villa",
  "description": "A 4-bedroom luxury villa with ocean view.",
  "location": "Mombasa, Kenya",
  "pricepernight": 120,
  "amenities": ["wifi", "pool", "kitchen"]
}
--- Validation:

--- Only authenticated users with role host can create.

--- pricepernight must be a positive decimal.

--- location, name, and description must be non-empty.

--- Output (Success):

json
Copy
Edit
{
  "message": "Property created successfully",
  "property_id": "uuid"
}
#### 2.2 Update Property
##### PUT /api/properties/:id

#### 2.3 Delete Property
##### DELETE /api/properties/:id

#### 2.4 Get Property by ID
##### GET /api/properties/:id

#### 2.5 Search Properties
##### GET /api/properties?location=Mombasa&guests=4&minPrice=50&maxPrice=200

### 3. Booking System
#### Functional Requirements
--- Guests can book available properties.

--- Prevent double bookings for the same dates.

--- Allow cancellation.

--- Track booking status: pending, confirmed, canceled, completed.

### API Endpoints
#### 3.1 Create Booking
##### POST /api/bookings

Input:

json
Copy
Edit
{
  "property_id": "uuid",
  "start_date": "2025-07-15",
  "end_date": "2025-07-20"
}
--- Validation:

--- Dates must be in the future.

--- end_date must be after start_date.

--- Property must be available for those dates.

--- Output (Success):

json
Copy
Edit
{
  "message": "Booking created successfully",
  "booking_id": "uuid"
}
#### 3.2 Cancel Booking
##### PUT /api/bookings/:id/cancel

#### 3.3 View Bookings (User)
##### GET /api/bookings?user_id=uuid

#### 3.4 View Bookings (Host)
GET /api/bookings?host_id=uuid

--- Performance Criteria
--- Average API response time < 500ms.

--- Database queries optimized with indexes on:

--- users.email, properties.location, bookings.property_id

--- Secure endpoints with middleware to enforce authentication and role-based access.

#### Security Considerations
#### All passwords hashed (bcrypt).

--- All endpoints protected using JWTs.

--- Input validation and sanitization on every route.

---Rate limiting and logging enabled for sensitive endpoints (e.g., login).
