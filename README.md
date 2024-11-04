# Todo List Application Documentation

## Overview
The Todo List Application is a simple yet powerful API-driven application designed to help users manage their tasks efficiently. Built with Laravel, it utilizes JWT for authentication and offers a straightforward RESTful interface for user registration, login, and task management.

## Features
- **User Registration**: Users can create an account by providing their name, email, and password.
- **User Login**: Users can log in to their accounts using their email and password.
- **Task Management**: Users can create, read, update, and delete their tasks.
- **JWT Authentication**: Secure user authentication using JSON Web Tokens.
- **Unit Testing**: Comprehensive unit tests ensure API functionality and reliability.
- **Error Handling**: Robust error handling implemented to provide meaningful feedback and appropriate HTTP status codes.

## Technologies Used
- **Backend**: Laravel 10.x
- **Authentication**: JWT (via `Tymon\JWTAuth`)
- **Database**: MySQL (or any preferred database)
- **Documentation**: OpenAPI (Swagger)

## API Endpoints

### Authentication

#### User Registration
- **Method**: `POST`
- **Endpoint**: `/api/auth/register`
- **Request Body**:
    ```json
    {
      "name": "Your Name",
      "email": "your.email@example.com",
      "password": "yourpassword",
      "password_confirmation": "yourpassword"
    }
    ```
- **Response**:
  - Success: `201 Created`
  - Error: `400 Bad Request`

#### User Login
- **Method**: `POST`
- **Endpoint**: `/api/auth/login`
- **Request Body**:
    ```json
    {
      "email": "your.email@example.com",
      "password": "yourpassword"
    }
    ```
- **Response**:
  - Success: `200 OK` with JWT token
  - Error: `401 Unauthorized`

#### Get User Info
- **Method**: `GET`
- **Endpoint**: `/api/auth/me`
- **Authorization**: Bearer Token required
- **Response**:
  - Success: `200 OK` with user information
  - Error: `401 Unauthorized`

#### Update User Info
- **Method**: `PUT`
- **Endpoint**: `/api/auth/update`
- **Authorization**: Bearer Token required
- **Request Body**:
    ```json
    {
      "name": "Updated Name",
      "email": "updated.email@example.com"
    }
    ```
- **Response**:
  - Success: `200 OK`
  - Error: `401 Unauthorized`, `400 Bad Request`

#### Logout
- **Method**: `POST`
- **Endpoint**: `/api/auth/logout`
- **Authorization**: Bearer Token required
- **Response**:
  - Success: `200 OK`
  - Error: `401 Unauthorized`

### CRUD Operations on Tasks

#### Create a New Task
- **Method**: `POST`
- **Endpoint**: `/api/tasks`
- **Request Body**:
    ```json
    {
      "description": "Task description",
      "due_date": "YYYY-MM-DD",
      "status": "pending"
    }
    ```
- **Response**:
  - Success: `201 Created`
  - Error: `400 Bad Request`

#### Retrieve All Tasks
- **Method**: `GET`
- **Endpoint**: `/api/tasks`
- **Response**:
  - Success: `200 OK` with a list of tasks

#### Retrieve a Specific Task
- **Method**: `GET`
- **Endpoint**: `/api/tasks/{id}`
- **Response**:
  - Success: `200 OK` with task details
  - Error: `404 Not Found`

#### Update a Specific Task
- **Method**: `PUT`
- **Endpoint**: `/api/tasks/{id}`
- **Request Body**:
    ```json
    {
      "description": "Updated description",
      "due_date": "YYYY-MM-DD",
      "status": "completed"
    }
    ```
- **Response**:
  - Success: `200 OK`
  - Error: `404 Not Found`, `400 Bad Request`

#### Delete a Specific Task (Soft Delete)
- **Method**: `DELETE`
- **Endpoint**: `/api/tasks/{id}`
- **Response**:
  - Success: `204 No Content`
  - Error: `404 Not Found`

## Installation
1. **Clone the repository**:
   ```bash
   git clone https://github.com/DahunsiJ/todo_api.git

2. **Navigate to the project directory**:

   ```bash
    cd todo_api
3. **Install dependencies**:

   ```bash
    composer install
4. **Configure your environment: Copy the .env.example file to .env and update the database and application settings.**

5. **Generate the application key**:

   ```bash
    php artisan key:generate
6. **Run migrations**:

   ```bash
    php artisan migrate
7. **Start the development server**:

   ```bash
    php artisan serve

## Documentation
API documentation is available at /api/documentation. It provides detailed information about each endpoint, including request and response formats.

## Unit Testing
To ensure functionality and reliability, unit tests have been implemented for all major API endpoints:

1. Authentication endpoints (register, login, logout)
2. CRUD operations on tasks (create, retrieve, update, delete)

1. **Run tests using**:

   ```bash
    php artisan test

The test suite covers expected behaviors, including successful operations and error handling for invalid requests.

## Error Handling
Robust error handling has been implemented to provide meaningful error messages with appropriate HTTP status codes. Validation errors return 400 Bad Request with specific error messages, unauthorized access returns 401 Unauthorized, and requests for non-existent resources return 404 Not Found.