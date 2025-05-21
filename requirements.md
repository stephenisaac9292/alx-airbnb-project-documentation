# Airbnb Clone – Backend Feature Requirements

---

## 1. User Authentication

### Description
Allows users to register, log in, and access secure areas of the system.

### API Endpoints
- `POST /api/register`: Registers a new user
- `POST /api/login`: Logs in an existing user
- `GET /api/user/profile`: Retrieves logged-in user data

### Input Specifications
- Email: required, must be valid
- Password: required, min 8 characters
- Username: optional, unique

### Output Specifications
- On success: JSON with user data and auth token
- On failure: Error message with status code

### Validation Rules
- Email must be unique
- Password must meet security standards (8+ chars, alphanumeric)
- Inputs must not be empty

### Performance Criteria
- Token issued within 500ms
- Auth checks must not exceed 300ms per request

---

## 2. Property Management

### Description
Allows hosts to list, update, and delete property listings.

### API Endpoints
- `POST /api/properties`: Create a new listing
- `PUT /api/properties/{id}`: Update a listing
- `DELETE /api/properties/{id}`: Delete a listing
- `GET /api/properties`: View all properties
- `GET /api/properties/{id}`: View property by ID

### Input Specifications
- Title, description, price, location: required
- Images: optional, max 5
- Availability: boolean

### Output Specifications
- Success: JSON object of property data
- Failure: Error message, 4xx or 5xx code

### Validation Rules
- Title must not exceed 100 characters
- Price must be a positive float
- User must be authenticated to manage properties

### Performance Criteria
- Retrieval of property list < 1s
- Image upload size per file: max 2MB

---

## 3. Booking System

### Description
Handles reservations made by guests.

### API Endpoints
- `POST /api/bookings`: Make a new booking
- `GET /api/bookings`: View user bookings
- `DELETE /api/bookings/{id}`: Cancel booking

### Input Specifications
- property_id: required
- start_date and end_date: required, valid format
- user_id: derived from token

### Output Specifications
- Success: Booking confirmation (JSON)
- Failure: Errors like "Date unavailable" or "Authentication required"

### Validation Rules
- Cannot book same property on same dates
- Booking dates must be in the future
- Auth required

### Performance Criteria
- Booking creation in < 700ms
- Search bookings per user in < 1s

---
