API Documentation for College-ERP
================================

### Introduction

The College-ERP API is a RESTful API built using Django framework. It provides endpoints for managing college data, including attendance, marks, and time tables.

### Available Endpoints

The following endpoints are available:

#### 1. Login

* **URL:** `/login/`
* **Method:** `POST`
* **Parameters:**
	+ `username`: string (required)
	+ `password`: string (required)
* **Return Type:** JSON
* **Description:** Logs in a user and returns a JSON response with a success message.
* **Usage Example:**
```bash
curl -X POST \
  http://127.0.0.1:8000/login/ \
  -H 'Content-Type: application/json' \
  -d '{"username": "samarth", "password": "project123"}'
```

#### 2. Get Attendance

* **URL:** `/attendance/`
* **Method:** `GET`
* **Parameters:**
	+ `start_date`: string (optional)
	+ `end_date`: string (optional)
* **Return Type:** JSON
* **Description:** Returns a JSON response with attendance data for the specified date range.
* **Usage Example:**
```bash
curl -X GET \
  http://127.0.0.1:8000/attendance/?start_date=2022-01-01&end_date=2022-01-31
```

#### 3. Get Marks

* **URL:** `/marks/`
* **Method:** `GET`
* **Parameters:**
	+ `student_id`: integer (required)
	+ `course_id`: integer (required)
* **Return Type:** JSON
* **Description:** Returns a JSON response with marks data for the specified student and course.
* **Usage Example:**
```bash
curl -X GET \
  http://127.0.0.1:8000/marks/?student_id=1&course_id=1
```

#### 4. Get Time Table

* **URL:** `/time_table/`
* **Method:** `GET`
* **Parameters:**
	+ `class_id`: integer (required)
* **Return Type:** JSON
* **Description:** Returns a JSON response with time table data for the specified class.
* **Usage Example:**
```bash
curl -X GET \
  http://127.0.0.1:8000/time_table/?class_id=1
```

#### 5. Create New User

* **URL:** `/users/`
* **Method:** `POST`
* **Parameters:**
	+ `username`: string (required)
	+ `password`: string (required)
	+ `role`: string (required)
* **Return Type:** JSON
* **Description:** Creates a new user and returns a JSON response with the user's details.
* **Usage Example:**
```bash
curl -X POST \
  http://127.0.0.1:8000/users/ \
  -H 'Content-Type: application/json' \
  -d '{"username": "newuser", "password": "project123", "role": "student"}'
```

### Error Handling

The API uses standard HTTP error codes to indicate errors. The following error codes are used:

* **400 Bad Request:** Invalid request parameters or syntax.
* **401 Unauthorized:** Invalid username or password.
* **403 Forbidden:** Access denied due to insufficient permissions.
* **404 Not Found:** Resource not found.
* **500 Internal Server Error:** Server-side error.

### Authentication

The API uses a simple authentication system based on username and password. To authenticate, send a `POST` request to the `/login/` endpoint with the `username` and `password` parameters.

### Notes

* The API is currently in beta and may be subject to changes.
* The API documentation is based on the available endpoints and may not be comprehensive.
* For more information, please refer to the reports included in the repository.