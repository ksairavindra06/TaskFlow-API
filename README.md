TaskFlow API

A REST API for managing tasks — create, update, filter by status, search by title, and delete — built with Spring Boot and Spring Data JPA.

Tech Stack
Java 17
Spring Boot 3
Spring Data JPA / Hibernate
H2 (local development) / PostgreSQL (production profile)
Bean Validation (Jakarta Validation)
JUnit 5 + Mockito
Docker
Features
Full CRUD for tasks (title, description, status, priority, due date)
Filter tasks by status (TODO, IN_PROGRESS, DONE)
Search tasks by title keyword
Request validation with clear, structured error responses
Global exception handling (404s, validation errors, unexpected errors)
Unit-tested service layer with Mockito
Running locally

Requires Java 17+ and Maven.

bash
mvn spring-boot:run

The app starts on http://localhost:8080 using an in-memory H2 database — no setup required. The H2 console is available at http://localhost:8080/h2-console (JDBC URL: jdbc:h2:mem:taskflowdb).

Running with Docker
bash
docker build -t taskflow-api .
docker run -p 8080:8080 taskflow-api
Running with PostgreSQL

Set environment variables and activate the postgres profile:

bash
export DB_HOST=localhost
export DB_PORT=5432
export DB_NAME=taskflowdb
export DB_USERNAME=your_username
export DB_PASSWORD=your_password

java -jar target/taskflow-api-1.0.0.jar --spring.profiles.active=postgres
Running tests
bash
mvn test
API Endpoints
Method	Endpoint	Description
GET	/api/tasks	List all tasks
GET	/api/tasks?status=TODO	Filter tasks by status
GET	/api/tasks?search=deploy	Search tasks by title
GET	/api/tasks/{id}	Get a single task
POST	/api/tasks	Create a task
PUT	/api/tasks/{id}	Update a task
DELETE	/api/tasks/{id}	Delete a task
Example: create a task
bash
curl -X POST http://localhost:8080/api/tasks \
  -H "Content-Type: application/json" \
  -d '{
    "title": "Set up CI pipeline",
    "description": "Add GitHub Actions for build and test",
    "priority": "HIGH",
    "dueDate": "2026-10-01"
  }'
Author

Sai Ravindra Kommineni — Portfolio · LinkedIn
