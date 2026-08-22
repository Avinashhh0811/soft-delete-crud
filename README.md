# Student Management System – Soft Delete CRUD

A simple **Student Management REST API** built using Spring Boot, Spring Data JPA, Hibernate, and MySQL.

This project demonstrates CRUD operations along with the **Soft Delete** concept, where records are marked as deleted instead of being permanently removed from the database.

## 🚀 Features

* Create Student
* Get Student by ID
* Get All Students
* Update Student
* Hard Delete Student
* Soft Delete Student
* MySQL database integration
* RESTful APIs
* JPA/Hibernate ORM
* Layered architecture

## 🛠️ Technologies Used

* Java 21
* Spring Boot 4.1.1
* Spring Web MVC
* Spring Data JPA
* Hibernate
* MySQL
* Maven
* REST API

## 📁 Project Structure

```text
soft-delete-crud/
│
├── src/
│   ├── main/
│   │   ├── java/
│   │   │   └── in/avinash/soft_delete_crud/
│   │   │       ├── Controller/
│   │   │       │   └── StudentController.java
│   │   │       │
│   │   │       ├── Entity/
│   │   │       │   └── Student.java
│   │   │       │
│   │   │       ├── Repository/
│   │   │       │   └── StudentRepository.java
│   │   │       │
│   │   │       ├── Service/
│   │   │       │   └── StudentService.java
│   │   │       │
│   │   │       └── SoftDeleteCrudApplication.java
│   │   │
│   │   └── resources/
│   │       └── application.properties
│   │
│   └── test/
│
├── pom.xml
└── README.md
```

## 🏗️ Architecture

The project follows a layered architecture:

```text
Client
   │
   ▼
Controller
   │
   ▼
Service
   │
   ▼
Repository
   │
   ▼
MySQL Database
```

### Controller Layer

Handles HTTP requests and API endpoints using REST annotations such as:

* `@RestController`
* `@GetMapping`
* `@PostMapping`
* `@PutMapping`
* `@DeleteMapping`
* `@PatchMapping`

### Service Layer

Contains the business logic for creating, retrieving, updating, hard deleting, and soft deleting students.

### Repository Layer

Uses `JpaRepository` to communicate with the MySQL database.

### Entity Layer

The `Student` class is mapped to a database table using JPA annotations.

## 🔗 API Endpoints

| Method | Endpoint                         | Description                |
| ------ | -------------------------------- | -------------------------- |
| POST   | `/api/students/create`           | Create student             |
| GET    | `/api/students/get/{id}`         | Get student by ID          |
| GET    | `/api/students/getAll`           | Get all active students    |
| PUT    | `/api/students/update/{id}`      | Update student             |
| DELETE | `/api/students/delete/{id}`      | Permanently delete student |
| PATCH  | `/api/students/delete-soft/{id}` | Soft delete student        |

## 📝 Create Student

### Request

```http
POST /api/students/create
```

### JSON

```json
{
  "name": "Avinash",
  "age": 22,
  "email": "avinash@example.com",
  "rollNo": 101,
  "mobileNo": "9876543210"
}
```

The application automatically sets:

```text
deleted = false
```

## 🔄 Update Student

```http
PUT /api/students/update/1
```

Example request:

```json
{
  "name": "Avinash Bachhav",
  "age": 23,
  "email": "avinash@example.com",
  "rollNo": 101,
  "mobileNo": "9876543210"
}
```

## 🗑️ Hard Delete vs Soft Delete

### Hard Delete

```http
DELETE /api/students/delete/1
```

The record is permanently removed from the database using:

```java
//studentRepository.deleteById(id);
```

### Soft Delete

```http
PATCH /api/students/delete-soft/1
```

Instead of removing the record, the application changes:

```text
deleted = false
```

to:

```text
deleted = true
```

The database record remains available, but it is excluded from normal queries.

This is useful when an application needs to preserve historical data.

## 🔍 Soft Delete Logic

The repository uses Spring Data JPA derived query methods:

```java
Optional<Student> findByIdAndDeletedIsFalse(Long id);

List<Student> findByAndDeletedIsFalse();
```

Therefore, only active records are returned.

```text
deleted = false  → Active
deleted = true   → Soft Deleted
```

## 🗄️ Database Configuration

Create a MySQL database:

```sql
CREATE DATABASE soft_delete_student;
```

Configure the database in `application.properties`:

```properties
spring.datasource.url=jdbc:mysql://localhost:3306/soft_delete_student
spring.datasource.username=root
spring.datasource.password=YOUR_PASSWORD

spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

> Do not upload real database passwords to GitHub. Use environment variables or a local configuration file for production projects.

## ▶️ How to Run

### 1. Clone the repository

```bash
git clone <YOUR_GITHUB_REPOSITORY_URL>
```

### 2. Open the project

Open the project in IntelliJ IDEA or your preferred Java IDE.

### 3. Configure MySQL

Create the database:

```sql
CREATE DATABASE soft_delete_student;
```

Update your MySQL username and password in `application.properties`.

### 4. Run the application

Run:

```text
SoftDeleteCrudApplication.java
```

The application will start on:

```text
http://localhost:8080
```

## 🧪 Testing

The APIs can be tested using:

* Postman
* Insomnia
* Thunder Client
* Browser for GET requests

Example:

```http
GET http://localhost:8080/api/students/getAll
```

## 📚 Concepts Covered

This project helped me understand and implement:

* **Spring Boot application setup**
* **REST API development**
* **CRUD operations**
* **Controller-Service-Repository architecture**
* **Dependency Injection**
* **Spring Data JPA**
* **Hibernate ORM**
* **JPA Entity Mapping**
* **MySQL database integration**
* **Derived Query Methods**
* **HTTP Methods – GET, POST, PUT, DELETE, PATCH**
* **`@PathVariable`**
* **`@RequestBody`**
* **`ResponseEntity`**
* **Hard Delete**
* **Soft Delete**
* **HTTP status handling**
* **Maven dependency management**

## 🔮 Future Improvements

* Add validation using Bean Validation
* Add global exception handling with `@ControllerAdvice`
* Add pagination and sorting
* Add search functionality
* Add restore API for soft-deleted students
* Add DTO layer
* Add Spring Security and JWT authentication
* Add unit and integration tests
* Add Swagger/OpenAPI documentation

## 👨‍💻 Author

**Avinash Bachhav**

MSc Computer Science | Java Backend Developer

**Skills:**
`Java` `Spring Boot` `Spring MVC` `Spring Data JPA` `Hibernate` `MySQL` `REST API` `Maven` `Git` `GitHub`

---

⭐ If you found this project useful, feel free to star the repository.
