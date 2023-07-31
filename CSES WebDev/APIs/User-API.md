## User API Documentation

This API provides endpoints for managing user data. It allows you to check if a user exists, create new users, retrieve user information, update user details, and delete users.

**1. Check if User Exists**
- **Endpoint:** `POST /api/v1/users/check`
- **Description:** Checks if a user with a specific email exists in the database.
- **Request Body:**
  ```json
  {
    "email": "user@example.com"
  }
  ```
- **Response:**
  - `200 OK` - User exists
    ```json
    {
      "exists": true,
      "user": { /* user data */ }
    }
    ```
  - `200 OK` - User does not exist
    ```json
    {
      "exists": false
    }
    ```
  - `400 Bad Request` - Invalid request body or missing email
    ```json
    {
      "message": "Failed",
      "errors": [ /* Array of validation errors */ ]
    }
    ```
  - `500 Internal Server Error` - Internal server error

**2. Create a New User**
- **Endpoint:** `POST /api/v1/users/create`
- **Description:** Creates a new user with the provided details.
- **Request Body:**
  ```json
  {
    "name": "John Doe",
    "email": "johndoe@example.com",
    "major": "Computer Science",
    "expectedGraduationYear": 2025
  }
  ```
- **Response:**
  - `201 Created` - User created successfully
    ```json
    {
      "name": "John Doe",
      "email": "johndoe@example.com",
      "major": "Computer Science",
      "expectedGraduationYear": 2025,
      "points": 0,
      "eventsAttended": [],
      "profilePicture": null
    }
    ```
  - `409 Conflict` - User with the same email already exists
    ```json
    {
      "message": "Email already exists"
    }
    ```
  - `500 Internal Server Error` - Internal server error

**3. Get User Information**
- **Endpoint:** `GET /api/v1/users/:email`
- **Description:** Retrieves information about a specific user using their email.
- **Response:**
  - `200 OK` - User found
    ```json
    {
      "name": "John Doe",
      "email": "johndoe@example.com",
      "major": "Computer Science",
      "expectedGraduationYear": 2025,
      "points": 50,
      "eventsAttended": [ /* Array of event IDs user attended */ ],
      "profilePicture": "https://example.com/profile.jpg"
    }
    ```
  - `404 Not Found` - User not found
    ```json
    {
      "message": "User not found"
    }
    ```
  - `500 Internal Server Error` - Internal server error

**4. Update User Details**
- **Endpoint:** `PUT /api/v1/users/:email`
- **Description:** Updates details of a specific user using their email.
- **Request Body:** (Optional, provide only the fields to be updated)
  ```json
  {
    "name": "John Updated",
    "major": "Computer Science (Updated)",
    "expectedGraduationYear": 2026
  }
  ```
- **Response:**
  - `200 OK` - User updated successfully
    ```json
    {
      "message": "Successful"
    }
    ```
  - `400 Bad Request` - Invalid request body or email
    ```json
    {
      "message": "Failed",
      "errors": [ /* Array of validation errors */ ]
    }
    ```
  - `404 Not Found` - User not found
    ```json
    {
      "message": "User not found"
    }
    ```
  - `500 Internal Server Error` - Internal server error

**5. Delete User**
- **Endpoint:** `DELETE /api/v1/users/:email`
- **Description:** Deletes a specific user using their email.
- **Response:**
  - `200 OK` - User deleted successfully
    ```json
    {
      "message": "Successful"
    }
    ```
  - `400 Bad Request` - Invalid email
    ```json
    {
      "message": "Failed",
      "errors": [ /* Array of validation errors */ ]
    }
    ```
  - `404 Not Found` - User not found
    ```json
    {
      "message": "User not found"
    }
    ```
  - `500 Internal Server Error` - Internal server error

**Note:** The `User` model is defined with the following schema:

```javascript
const userSchema = new mongoose.Schema({
  email: { type: String, required: true, unique: true },
  name: { type: String, required: true },
  major: { type: String, required: true },
  expectedGraduationYear: { type: Number, required: true },
  points: { type: Number, default: 0 },
  eventsAttended: {
    type: [{
      type: mongoose.Schema.Types.ObjectId,
      ref: 'Event',
    }],
    default: [],
  },
  profilePicture: { type: String },
});
```
