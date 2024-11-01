---
toc: false
layout: post
title: Project Backend Overview
type: collab
permalink: /projectbackendoverview
courses: {csa: {week: 10}}
---

---
toc: false
layout: post
title: Project Backend Overview
type: collab
permalink: /projectbackendoverview
courses: {csa: {week: 10}}
---

# Student Management API Documentation

## Overview
This project implements a RESTful API for managing student data. It provides endpoints to create, retrieve, update, and delete student records, along with specific methods for searching and modifying student tasks based on various criteria.

## Key Features

### 1. **Student Creation**
   - **Endpoint:** `POST /api/students/create`
   - **Description:** Allows users to create a new student entry.
   - **Process:**
      - Accepts a JSON body representing the student.
      - Checks if a student with the same `username` already exists to prevent duplicate records.
      - Stores the new student record in the database.
   - **Sample Request Body:**
     ```json
     {
       "name": "Srinivas Nampalli",
       "username": "srininampalli",
       "tableNumber": 4,
       "course": "CSA",
       "tasks": ["Task 1", "Task 2"],
       "trimester": 1,
       "period": 3
     }
     ```
   - **Response Codes:** 
     - `200 OK` on successful creation
     - `400 Bad Request` if a duplicate student exists

### 2. **Retrieve All Students**
   - **Endpoint:** `GET /api/students/all`
   - **Description:** Fetches a list of all students.
   - **Process:** Directly retrieves all student records from the database.
   - **Response Example:**
     ```json
     [
       {
         "id": 1,
         "name": "Srinivas Nampalli",
         "username": "srininampalli",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       },
       {
         "id": 2,
         "name": "Aditya Samavedam",
         "username": "adityasamavedam",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       },
       {
         "id": 3,
         "name": "Nitin Balaji",
         "username": "nitinsandiego",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       }
     ]
     ```

### 3. **Retrieve Student by Criteria**
   - **Endpoint:** `GET /api/students/find`
   - **Description:** Finds a student by matching `name`, `course`, `trimester`, and `period`.
   - **Process:**
     - Queries the database to match a student's criteria.
   - **Query Parameters:** `name`, `course`, `trimester`, `period`
   - **Response Example:**
     ```json
     {
       "id": 1,
       "name": "Srinivas Nampalli",
       "username": "srininampalli",
       "tableNumber": 4,
       "course": "CSA",
       "tasks": ["Task 1", "Task 2"],
       "trimester": 1,
       "period": 3
     }
     ```

### 4. **Retrieve Team by Table**
   - **Endpoint:** `GET /api/students/findteam`
   - **Description:** Finds a group of students seated at the same table in a given `course`, `trimester`, `period`, and `table`.
   - **Query Parameters:** `course`, `trimester`, `period`, `table`
   - **Response Example:**
     ```json
     [
       {
         "id": 1,
         "name": "Srinivas Nampalli",
         "username": "srininampalli",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       },
       {
         "id": 2,
         "name": "Aditya Samavedam",
         "username": "adityasamavedam",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       },
       {
         "id": 3,
         "name": "Nitin Balaji",
         "username": "nitinsandiego",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       }
     ]
     ```

### 5. **Retrieve Students by Period**
   - **Endpoint:** `GET /api/students/findperiod`
   - **Description:** Finds all students for a specific `course`, `trimester`, and `period`.
   - **Query Parameters:** `course`, `trimester`, `period`
   - **Response Example:**
     ```json
     [
       {
         "id": 1,
         "name": "Srinivas Nampalli",
         "username": "srininampalli",
         "tableNumber": 4,
         "course": "CSA",
         "tasks": ["Task 1", "Task 2"],
         "trimester": 1,
         "period": 3
       },
       ...
     ]
     ```

### 6. **Update Tasks for a Student**
   - **Endpoint:** `POST /api/students/updatetasks`
   - **Description:** Updates the task list for a student identified by `username`.
   - **Process:** 
     - Accepts `username` and new `tasks` array in the request body.
     - Updates the `tasks` field for the student in the database.
   - **Sample Request Body:**
     ```json
     {
       "username": "srininampalli",
       "tasks": ["Task 1 - Completed", "Task 2"]
     }
     ```
   - **Response Codes:** 
     - `200 OK` on successful update
     - `404 Not Found` if the student doesn’t exist

### 7. **Delete Student by Username**
   - **Endpoint:** `DELETE /api/students/delete`
   - **Description:** Deletes a student based on their `username`.
   - **Process:** 
     - Locates the student by `username` and deletes them from the database.
   - **Query Parameter:** `username`
   - **Response Example:**
     ```json
     {
       "message": "Student with username 'srininampalli' has been deleted."
     }
     ```

### 8. **Mark Task as Completed**
   - **Endpoint:** `POST /api/students/completeTask`
   - **Description:** Marks a specific task as completed for a student identified by `username`.
   - **Process:**
     - Locates the student by `username`.
     - Finds the specified `task` and marks it as completed by appending " - Completed" to the task name.
   - **Query Parameters:** `username`, `task`
   - **Response Example:**
     ```json
     {
       "id": 1,
       "name": "Srinivas Nampalli",
       "username": "srininampalli",
       "tasks": ["Task 1 - Completed", "Task 2"],
       ...
     }
     ```

## Summary of Changes and Additions

1. **Controller Methods:** Added methods for all CRUD operations and specific queries (retrieve by criteria, find team, update tasks, etc.).
2. **Student Service:** Centralized business logic for student operations, such as creation, deletion, and task updates.
3. **JPA Repository:** Extended with custom query methods:
   - `findByNameCourseTrimesterPeriod` - Finds students based on detailed criteria.
   - `findTeam` - Retrieves students based on `table`, `course`, `trimester`, and `period`.
   - `findPeriod` - Retrieves students based on `course`, `trimester`, and `period`.

## Testing and Troubleshooting
To ensure the API functions correctly:
- **Testing:** Use tools like Postman or curl to send HTTP requests to each endpoint.
- **Error Handling:** Implemented error handling in the service layer to avoid duplicates and handle missing students with appropriate status codes (`400` for bad requests, `404` for not found, etc.).
- **Transaction Management:** Some methods, such as marking a task as completed, are marked `@Transactional` to maintain data consistency.