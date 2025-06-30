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

{
  "message": "User registered successfully",
  "token": "JWT_TOKEN_HERE"
}
### Output (Failure):

<--json-->
<--Copy-->
<--Edit-->
{
  "error": "Email already in use"
}

<--1.2 Login User-->
<--POST /api/auth/login-->

{
  "email": "user@example.com",
  "password": "securePassword123"
}
<--Output (Success):-->

{
  "token": "JWT_TOKEN_HERE",
  "user": {
    "id": "uuid",
    "role": "guest"
  }
}

<--Property Management-->
<--Functional Requirements-->
<--Hosts can create, update, or delete their property listings.-->

<--Guests can view and filter listings.-->

<--Listings include title, description, price, location, amenities, images.-->

<--2.1 Create Property-->
<--POST /api/properties-->

{
  "name": "Modern Villa",
  "description": "A 4-bedroom luxury villa with ocean view.",
  "location": "Mombasa, Kenya",
  "pricepernight": 120,
  "amenities": ["wifi", "pool", "kitchen"]
}

{
  "message": "Property created successfully",
  "property_id": "uuid"
}

<--2.2 Update Property-->
 <--PUT /api/properties/:id-->

<--2.3 Delete Property-->
<--DELETE /api/properties/:id-->

<--2.4 Get Property by ID-->
<--GET /api/properties/:id-->

<--2.5 Search Properties-->
 <--GET /api/properties?location=Mombasa&guests=4&minPrice=50&maxPrice=200-->

 <--3. Booking System-->
 <--Functional Requirements-->

<--API Endpoints-->
 <--3.1 Create Booking-->
 <--POST /api/bookings-->

{
  "property_id": "uuid",
  "start_date": "2025-07-15",
  "end_date": "2025-07-20"
}

{
  "message": "Booking created successfully",
  "booking_id": "uuid"
}
 <--3.2 Cancel Booking-->
 <--PUT /api/bookings/:id/cancel-->

 <--3.3 View Bookings (User)-->
 <--GET /api/bookings?user_id=uuid-->

 <--3.4 View Bookings (Host)-->
<--GET /api/bookings?host_id=uuid-->

<--Security Considerations-->
 <--All passwords hashed (bcrypt).-->
