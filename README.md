# API Documentation - Complaint Management System

## Overview

This API manages orders, notifications, products, users, and complaints in the complaint management system.

All endpoints accept and respond with **JSON**.

Ensure all body requests are sent with header:

```http
Content-Type: application/json
```

Errors will include detailed messages depending on the server-side failure.

Authentication protection (e.g., tokens) is recommended but not covered in this documentation.

---

## Summary of Routes

| Resource | Method | Endpoint | Description |
|:---|:---|:---|:---|
| Order | GET | `/orders/:id` | Get order by ID |
| Order | POST | `/orders/` | Add a new order |
| Notification | GET | `/notifications/:id` | Get notification by ID |
| Notification | POST | `/notifications/` | Add a new notification |
| Product | GET | `/products/:id` | Get product by ID |
| Product | POST | `/products/` | Add a new product |
| Product | PUT | `/products/:id` | Update product by ID |
| Product | DELETE | `/products/:id` | Delete product by ID |
| User | GET | `/users/:id` | Get user by ID |
| User | POST | `/users/` | Add a new user |
| User | PUT | `/users/:id` | Update user by ID |
| User | DELETE | `/users/:id` | Delete user by ID |
| Complaint | GET | `/complaints/:id` | Get complaint by ID |
| Complaint | POST | `/complaints/` | Add a new complaint |
| Complaint | PUT | `/complaints/:id` | Update complaint status |
| Complaint | DELETE | `/complaints/:id` | Delete complaint by ID |

---

## API Details

### 1. Order API

#### GET `/orders/:id`
- **Description:** Retrieve an order by ID.
- **Parameters:**
  - `id` (URL, Integer, Required): Order ID
- **Responses:**
  - `200 OK`
    ```json
    {
      "order_id": 1,
      "user_id": 2,
      "product_id": 3,
      "request_type": "purchase",
      "status": "pending"
    }
    ```
  - `404 Not Found`
    ```json
    { "message": "Order not found" }
    ```
  - `500 Internal Server Error`
    ```json
    { "message": "Error retrieving order", "error": "details" }
    ```

#### POST `/orders/`
- **Description:** Add a new order.
- **Body Parameters:**
  - `userId` (Integer, Required)
  - `productId` (Integer, Required)
  - `requestType` (String, Required)
  - `status` (String, Required)
- **Responses:**
  - `201 Created`
    ```json
    { "message": "Order added successfully", "orderId": 1 }
    ```
  - `500 Internal Server Error`
    ```json
    { "message": "Error adding order", "error": "details" }
    ```

---

### 2. Notification API

#### GET `/notifications/:id`
- **Description:** Retrieve a notification by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
    ```json
    {
      "notification_id": 1,
      "user_id": 2,
      "complaint_id": 3,
      "message": "New update available",
      "status": "unread"
    }
    ```
  - `404 Not Found`
  - `500 Internal Server Error`

#### POST `/notifications/`
- **Description:** Add a new notification.
- **Body Parameters:**
  - `userId` (Integer, Required)
  - `complaintId` (Integer, Required)
  - `message` (String, Required)
  - `status` (String, Required)
- **Responses:**
  - `201 Created`
  - `500 Internal Server Error`

---

### 3. Product API

#### GET `/products/:id`
- **Description:** Retrieve a product by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
    ```json
    {
      "product_id": 1,
      "name": "Product Name",
      "type": "Electronics",
      "location": "Warehouse A",
      "status": "available",
      "description": "A high quality product"
    }
    ```
  - `404 Not Found`
  - `500 Internal Server Error`

#### POST `/products/`
- **Description:** Add a new product.
- **Body Parameters:**
  - `name` (String, Required)
  - `type` (String, Required)
  - `location` (String, Required)
  - `status` (String, Required)
  - `description` (String, Required)
- **Responses:**
  - `201 Created`
  - `500 Internal Server Error`

#### PUT `/products/:id`
- **Description:** Update a product by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Body Fields (Optional):** `name`, `type`, `location`, `status`, `description`
- **Responses:**
  - `200 OK`
  - `500 Internal Server Error`

#### DELETE `/products/:id`
- **Description:** Delete a product by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
  - `500 Internal Server Error`

---

### 4. User API

#### GET `/users/:id`
- **Description:** Retrieve a user by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
    ```json
    {
      "user_id": 1,
      "name": "John Doe",
      "email": "john@example.com"
    }
    ```
  - `404 Not Found`
  - `500 Internal Server Error`

#### POST `/users/`
- **Description:** Add a new user.
- **Body Parameters:**
  - `name` (String, Required)
  - `email` (String, Required)
  - `password` (String, Required)
- **Responses:**
  - `201 Created`
  - `500 Internal Server Error`

#### PUT `/users/:id`
- **Description:** Update a user by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Body Fields (Optional):** `name`, `email`
- **Responses:**
  - `200 OK`
  - `500 Internal Server Error`

#### DELETE `/users/:id`
- **Description:** Delete a user by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
  - `500 Internal Server Error`

---

### 5. Complaint API

#### GET `/complaints/:id`
- **Description:** Retrieve a complaint by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
    ```json
    {
      "complaint_id": 1,
      "user_id": 123,
      "product_id": 456,
      "complaint_text": "Product was damaged during shipping",
      "status": "pending"
    }
    ```
  - `404 Not Found`
  - `500 Internal Server Error`

#### POST `/complaints/`
- **Description:** Add a new complaint.
- **Body Parameters:**
  - `userId` (Integer, Required)
  - `productId` (Integer, Required)
  - `complaintText` (String, Required)
  - `status` (String, Required)
- **Responses:**
  - `201 Created`
  - `500 Internal Server Error`

#### PUT `/complaints/:id`
- **Description:** Update complaint status.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Body Parameter:**
  - `status` (String, Required)
- **Responses:**
  - `200 OK`
  - `500 Internal Server Error`

#### DELETE `/complaints/:id`
- **Description:** Delete a complaint by ID.
- **Parameters:**
  - `id` (URL, Integer, Required)
- **Responses:**
  - `200 OK`
  - `500 Internal Server Error`

---

## Data Models

### Complaint
| Field | Type | Description |
|:------|:-----|:------------|
| complaint_id | Integer | Unique complaint ID |
| user_id | Integer | User who filed the complaint |
| product_id | Integer | Product related to the complaint |
| complaint_text | String | Complaint details |
| status | String | Status of the complaint |

### Order
| Field | Type | Description |
|:------|:-----|:------------|
| order_id | Integer | Unique order ID |
| user_id | Integer | User who made the order |
| product_id | Integer | Ordered product ID |
| request_type | String | Type of request (purchase, rent) |
| status | String | Order status |

### Notification
| Field | Type | Description |
|:------|:-----|:------------|
| notification_id | Integer | Unique notification ID |
| user_id | Integer | Receiving user ID |
| complaint_id | Integer | Related complaint ID |
| message | String | Notification message |
| status | String | Status of notification |

### Product
| Field | Type | Description |
|:------|:-----|:------------|
| product_id | Integer | Unique product ID |
| name | String | Name of the product |
| type | String | Product category/type |
| location | String | Storage location |
| status | String | Availability status |
| description | String | Detailed description |

### User
| Field | Type | Description |
|:------|:-----|:------------|
| user_id | Integer | Unique user ID |
| name | String | Full name |
| email | String | Email address |
| password | String | Encrypted password (not returned in API response) |

---

## Notes

- All request and response payloads use **JSON** format.
- Make sure to send `Content-Type: application/json` header.
- Error responses include helpful messages.
- Implement security (authentication tokens) for protected endpoints.
