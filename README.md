# TaskFlow – Task Management API

A REST API for managing users and tasks, built with Node.js, Express.js, and MongoDB.

## Technologies

- Node.js
- Express.js 5
- MongoDB
- Mongoose
- Docker
- Docker Compose
- GitHub Actions
- Node.js Test Runner

## Features

- Create and retrieve users
- Delete users
- Create and retrieve tasks
- Update and delete tasks
- Input validation
- HTTP Status Code handling
- Centralized error handling
- Automated API testing
- CI/CD pipeline with GitHub Actions
- Docker containerization

## API Endpoints

### Users

| Method | Endpoint       | Description   | Status Code   |
| ------ | -------------- | ------------- | ------------- |
| GET    | /api/users     | Get all users | 200           |
| POST   | /api/users     | Create user   | 201, 400      |
| GET    | /api/users/:id | Get user      | 200, 400, 404 |
| DELETE | /api/users/:id | Delete user   | 200, 400, 404 |

### Tasks

| Method | Endpoint       | Description   | Status Code   |
| ------ | -------------- | ------------- | ------------- |
| GET    | /api/tasks     | Get all tasks | 200           |
| POST   | /api/tasks     | Create task   | 201, 400      |
| GET    | /api/tasks/:id | Get task      | 200, 400, 404 |
| PUT    | /api/tasks/:id | Update task   | 200, 400, 404 |
| DELETE | /api/tasks/:id | Delete task   | 200, 400, 404 |

Task fields: `title` (required), `description`, `status` (`todo`, `in-progress`, `done`), `priority` (`low`, `medium`, `high`), `assignedTo` (user ID).

## HTTP Status Codes

| Code | Meaning                        |
| ---- | ------------------------------ |
| 200  | OK - Successful request        |
| 201  | Created - Resource created     |
| 400  | Bad Request - Invalid input    |
| 404  | Not Found - Resource not found |
| 500  | Internal Server Error          |

## Automated Testing

TaskFlow uses the built-in Node.js Test Runner (`node:test`) for automated API testing.

Run tests:

```
npm test
```

### Test Cases

| Test ID | Description               |
| ------- | ------------------------- |
| TC-01   | Home endpoint response    |
| TC-02   | Create a task             |
| TC-03   | Retrieve all tasks        |
| TC-04   | Retrieve a task by ID     |
| TC-05   | Update a task             |
| TC-06   | Delete a task             |
| TC-07   | Reject invalid task input |
| TC-08   | Reject invalid task ID    |
| TC-09   | Handle non-existing tasks |

Tests use a separate MongoDB database named `taskdb_test`.

## CI/CD Pipeline

GitHub Actions is used to automate testing and Docker image building.

The pipeline runs automatically on:

- Push to the main branch
- Pull requests targeting the main branch

### Pipeline Flow

```
     Code Push / Pull Request
                |
                v
         GitHub Actions
                |
                v
         Checkout Code
                |
                v
          Setup Node.js
                |
                v
       Install Dependencies
                |
                v
          Start MongoDB
                |
                v
       Run Automated Tests
                |
           +----+----+
           |         |
          PASS      FAIL
           |         |
           v         v
       Docker Build  Stop
           |
           v
     Pipeline Success
```

If automated tests fail, the pipeline stops and the Docker image is not built.

More details: [docs/ci-cd-flow.md](docs/ci-cd-flow.md)

## Docker Commands

Build and run:

```
docker compose up --build -d
```

Check containers:

```
docker ps
```

View logs:

```
docker compose logs
```

Stop containers:

```
docker compose down
```

## Run Locally

Install dependencies:

```
npm install
```

Start server (MongoDB must be running on `localhost:27017`):

```
npm start
```

The server runs on port 3000.

Environment variables:

| Variable        | Default                              | Description                    |
| --------------- | ------------------------------------ | ------------------------------ |
| PORT            | 3000                                 | Server port                    |
| MONGO_URI       | mongodb://localhost:27017/taskdb     | MongoDB connection string      |
| MONGO_URI_TEST  | mongodb://localhost:27017/taskdb_test | MongoDB URI used by the tests |

## Project Structure

```
TaskFlow/
├── src/
│   └── server.js
├── tests/
│   └── task.test.js
├── docs/
│   └── ci-cd-flow.md
├── .github/
│   └── workflows/
│       └── ci.yml
├── .dockerignore
├── .gitignore
├── Dockerfile
├── docker-compose.yml
├── package.json
└── README.md
```
