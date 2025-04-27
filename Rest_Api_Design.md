# REST API Design for a Marketplace

## 1. Introduction
This document presents the design of a RESTful API for a Marketplace. 
The API manages products, users, and categories, enabling users to search, filter, and manage products efficiently.

## 2. Entities
### 2.1 Product
- `id` (UUID, unique identifier)
- `title` (String, required)
- `description` (String required)
- `price` (BigDecimal required)
- `city` (String, required)
- `date` (Date, required)
- `user_id` (UUID, foreign key to users)

### 2.2 User
- `id` (UUID, unique identifier)
- `email` (String,unique, required)
- `birth_date` (Date, optional)
- `phone` (String, unique, required)
- `password` (String, required)


## 3. API Endpoints
### 3.1 Books
**GET /products**
- Returns a paginated list of books.
- Filters: `title` 
- HATEOAS links provided for navigation.

**POST /products**
- Creates a product.
- Requires authentication.
- HATEOAS links included in the response.

**GET /products/{id}**
- Retrieves a single product by its ID.
- HATEOAS links included.

**PUT /products/{id}**
- Updates product details.
- Requires authentication.
- HATEOAS links included.

**DELETE /product/{id}**
- Deletes a product.
- Requires authentication.
- HATEOAS links included.

### 3.2 User
**GET /users**
- Returns a paginated list of authors.
- Filters: `name` .
- HATEOAS links included.

**POST /users**
- Creates a users.
- Requires authentication.
- HATEOAS links included.

**GET /users/{id}**
- Retrieves a user by ID.
- HATEOAS links included.
  
## 4. Functional & Non-functional Requirements
### Functional:
- CRUD operations for products, users.
- Filtering, sorting, and pagination support.
- Secure access control for modifications.
- HATEOAS for API discoverability.

### Non-functional:
- API must follow RESTful principles.
- High availability and performance optimizations.
- Caching for frequent queries.
- JWT authentication with token expiration handling.

## 5. Richardson Maturity Model
- **Level 1**: Resources represented as URLs.
- **Level 2**: Proper HTTP methods (`GET`, `POST`, `PUT`, `DELETE`).
- **Level 3**: Full HATEOAS support for discoverability.

## 6. Error Handling
- `400 Bad Request` – Invalid input.
- `401 Unauthorized` – Authentication failure.
- `403 Forbidden` – Access denied.
- `404 Not Found` – Resource not found.
- `429 Too Many Requests` – Rate limit exceeded.
- `500 Internal Server Error` – Unexpected server issue.

## 7. Authentication & Authorization
- Uses JWT-based authentication.
- Admin roles required for write operations.
- Role-based access control (RBAC) is implemented.

## 8. Pagination
- Default: 10 items per page.
- Query params: `?page=1&size=10`.
- HATEOAS links provided for pagination.

## 9. Caching Strategy
- Books list cached using ETag and Last-Modified headers.
- Frequent GET requests use Redis caching.
- Cache invalidation upon updates.
- Explanation of non-cached endpoints included. 
---
This API follows industry standards to ensure maintainability, scalability, and efficiency.

