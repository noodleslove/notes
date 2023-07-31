## User APIs
---

**1. Check if a User Exists**

Endpoint: `/api/v1/users/check`
Method: POST
Description: Check if a user with the given email exists in the database.

Request Body:
```json
{
  "email": "user@example.com"
}
```

Response:
```json
{
  "exists": true,
  "user": {
    "_id": "user_id",
    "name": "John Doe",
    "email": "user@example.com",
    "major": "Computer Science",
    "expectedGraduationYear": 2024,
    "points": 100,
    "eventsAttended": ["event_id1", "event_id2"],
    "profilePicture": "base64_encoded_image"
  }
}
```

---

**2. Create a New User**

Endpoint: `/api/v1/users/create`
Method: POST
Description: Create a new user in the database.

Request Body:
```json
{
  "name": "John Doe",
  "email": "user@example.com",
  "major": "Computer Science",
  "expectedGraduationYear": 2024
}
```

Response:
```json
{
  "_id": "user_id",
  "name": "John Doe",
  "email": "user@example.com",
  "major": "Computer Science",
  "expectedGraduationYear": 2024,
  "points": 0,
  "eventsAttended": [],
  "profilePicture": null
}
```

---

**3. Get User Information**

Endpoint: `/api/v1/users/:email`
Method: GET
Description: Get information about a specific user based on their email.

Response:
```json
{
  "_id": "user_id",
  "name": "John Doe",
  "email": "user@example.com",
  "major": "Computer Science",
  "expectedGraduationYear": 2024,
  "points": 100,
  "eventsAttended": ["event_id1", "event_id2"],
  "profilePicture": "base64_encoded_image"
}
```

---

**4. Update User Information**

Endpoint: `/api/v1/users/:email`
Method: PUT
Description: Update information for a specific user based on their email.

Request Body (example to update the name and major):
```json
{
  "name": "Jane Doe",
  "major": "Electrical Engineering"
}
```

Response:
```json
{
  "message": "Successful"
}
```

---

**5. Delete User**

Endpoint: `/api/v1/users/:email`
Method: DELETE
Description: Delete a user based on their email.

Response:
```json
{
  "message": "Successful"
}
```

---

Please note that for updating and deleting a user, you need to pass the user's email as a URL parameter. The APIs use the HTTP status codes to indicate the success or failure of each operation.

Additionally, you can handle file uploads for the profile picture by sending the image data in base64 format in the request body when creating or updating a user. In the response, the profile picture is also provided in base64 encoded format.

Ensure that you implement proper error handling and authentication mechanisms in your actual server-side code to protect sensitive user data and handle different edge cases.