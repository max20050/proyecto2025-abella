# Proyecto2025-Abella

> ⚠️ **Disclaimer:** This was my first Go (Golang) project following a layered architecture for a web application. The sole purpose of this project was **learning** — specifically to understand how to structure a web app using the Controller → Service → DAO pattern in Go. Code quality, best practices, and production-readiness were not the focus. Please keep that in mind when reading through the codebase.

---

## What is this?

A full-stack **gym management web app** built as part of the **Software Architecture 1** course at UCC (Universidad Católica de Córdoba). The application allows gym members to browse activities offered by the gym and reserve a spot in them.

---

## Features

- View all available gym activities
- Reserve a spot in an activity (inscription)
- User management (registration / lookup)
- Activity management (create and list activities with available capacity)
- Inscription management (enroll a user into an activity, view enrollments)

---

## Tech Stack

| Layer | Technology |
|---|---|
| Backend | Go (Golang) |
| HTTP Framework | [Gin](https://github.com/gin-gonic/gin) |
| ORM | [GORM](https://gorm.io/) |
| Database | MySQL |
| Frontend | React |
| Containerization | Docker / Docker Compose |

---

## Architecture

The project is a **monolith** composed of three internal services:

| Service | Responsibility |
|---|---|
| **Users** | Manages gym member data |
| **Activities** | Manages gym activities and their available capacity |
| **Inscriptions** | Handles reservations — linking users to activities |

Each service follows the same layered pattern:

```
Controller → Service → DAO
```

- **Controller** — handles incoming HTTP requests and returns responses (via Gin)
- **Service** — contains business logic and orchestrates calls to the data layer
- **DAO (Data Access Object)** — abstracts all database operations, built on top of GORM

Supporting layers shared across services:

- **Domain** — defines the core data models and structs
- **Clients** — handles communication between internal services
- **Utils** — shared helpers and utilities

---

## Project Structure

```
Proyecto2025-Abella/
├── backend/
│   ├── app/              # App bootstrap and router setup
│   ├── clients/          # Inter-service communication
│   ├── controller/       # HTTP handlers (Gin)
│   ├── dao/              # Data Access Objects (GORM + MySQL)
│   ├── domain/           # Data models and structs
│   ├── services/         # Business logic
│   ├── utils/            # Shared helpers
│   ├── Dockerfile
│   ├── go.mod
│   ├── go.sum
│   └── main.go
├── frontend/             # React client
├── sql/                  # MySQL schema and seed scripts
└── docker-compose.yml
```

---

## Getting Started

### Prerequisites
- [Docker](https://www.docker.com/) and [Docker Compose](https://docs.docker.com/compose/) installed on your machine.

### Running the app

```bash
# Clone the repository
git clone https://github.com/Max20050/Proyecto2025-Abella.git
cd Proyecto2025-Abella

# Start all services (backend, frontend, MySQL)
docker-compose up --build
```

Docker Compose will spin up the Go backend, the React frontend, and the MySQL database together.

---

## Purpose & Learning Goals

This project was built with the following learning objectives:

- Understand the **Controller → Service → DAO** layered pattern in Go
- Learn how to structure a monolithic web application split into logical internal services
- Get hands-on experience with **Gin** as an HTTP router and request handler
- Use **GORM** to interact with a **MySQL** database through a DAO layer
- Separate domain models, business logic, and data access into distinct layers
- Build a **React** frontend that consumes a Go REST API
- Containerize a multi-service application with **Docker Compose**

---

## Acknowledgements

Forked from [UCC-ArqSoft1/Proyecto2025-Abella](https://github.com/UCC-ArqSoft1/Proyecto2025-Abella) as part of the Software Architecture 1 course curriculum.
