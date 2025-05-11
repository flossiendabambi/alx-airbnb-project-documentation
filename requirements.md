# Airbnb Clone Backend – Technical & Functional Requirements

## Feature 1: User Authentication

### Functional Requirements:
- Users can register with email, password, first name, last name, and phone number (optional).
- Users can log in and receive a session token (JWT).
- Only authenticated users can access protected endpoints.

### API Endpoints:
- `POST /api/v1/register`  
  - Input: JSON (email, password, first_name, last_name, phone_number)
  - Output: 201 Created / 400 Bad Request / 409 Conflict
- `POST /api/v1/login`  
  - Input: JSON (email, password)
  - Output: 200 OK + JWT Token / 401 Unauthorized
- `GET /api/v1/profile`  
  - Output: User profile (requires token)

### Validation Rules:
- Email must be unique and valid.
- Password must be at least 8 characters.
- All fields required except phone_number.

### Performance:
- Token generation in < 500ms.
- Rate limiting on login to prevent brute force.

---

## Feature 2: Property Management

### Functional Requirements:
- Hosts can create, update, and delete their properties.
- Guests can view all available properties.

### API Endpoints:
- `POST /api/v1/properties`  
  - Input: JSON (name, location, price_per_night, description)
  - Output: 201 Created / 400 Bad Request
- `GET /api/v1/properties`  
  - Output: List of all properties (paginated)
- `PUT /api/v1/properties/:id`  
  - Input: Updated JSON
  - Output: 200 OK / 403 Forbidden
- `DELETE /api/v1/properties/:id`  
  - Output: 204 No Content / 403 Forbidden

### Validation Rules:
- Only hosts can manage properties.
- Price must be a positive decimal.
- Location must be present and non-empty.

### Performance:
- Paginated property retrieval: 20 per page, load < 300ms.

---

## Feature 3: Booking System

### Functional Requirements:
- Users can book properties for specific date ranges.
- Prevent double-booking of properties.

### API Endpoints:
- `POST /api/v1/bookings`  
  - Input: JSON (property_id, start_date, end_date)
  - Output: 201 Created / 400 Bad Request / 409 Conflict
- `GET /api/v1/bookings/:user_id`  
  - Output: List of user's bookings

### Validation Rules:
- Date range must be valid and in the future.
- Property must be available for the requested dates.

### Performance:
- Booking conflict check within 100ms.
- Return booking confirmation instantly after payment.

---

## General Notes:
- All endpoints should be RESTful and return JSON.
- Authentication should use JWT for session management.
- All endpoints must include error handling and logging.

