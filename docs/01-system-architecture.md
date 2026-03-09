# ADNest — System Architecture

## Table of Contents

1. [Architecture Overview](#architecture-overview)
2. [Repository Structure](#repository-structure)
3. [Frontend Architecture](#frontend-architecture)
4. [Backend Architecture](#backend-architecture)
5. [API Communication](#api-communication)
6. [API Documentation](#api-documentation)
7. [Database](#database)
8. [Security](#security)
9. [Development Philosophy](#development-philosophy)

---

## Architecture Overview

ADNest follows a modern **client-server architecture**.

The system is composed of two main applications:

1. **Frontend** (Client)
2. **Backend** (Server)

These applications are maintained inside a **monorepo**.

| Layer    | Responsibility                                         |
| -------- | ------------------------------------------------------ |
| Frontend | User interface and user interaction                    |
| Backend  | Business logic, data persistence, and security         |

Communication between the two systems happens through a **REST API**.

---

## Repository Structure

The project follows a monorepo structure:

```
adnest/
├── client/         # Astro + React frontend
├── server/         # Spring Boot API
├── docs/           # System documentation for development
└── README.md
```

---

## Frontend Architecture

The frontend is built using **Astro with React components**. Astro provides the page structure and routing, while React is used for interactive UI components.

### Technologies

| Technology  | Purpose                  |
| ----------- | ------------------------ |
| Astro       | Page structure & routing |
| React       | Interactive UI components|
| TypeScript  | Type safety              |
| TailwindCSS | Styling                  |
| Vite        | Build tooling            |

### Directory Structure

```
client/src/
├── assets/
├── components/
│   ├── ui/
│   ├── charts/
│   └── forms/
├── layouts/
├── pages/
├── services/
└── styles/
```

### Responsibilities

- UI rendering
- User interaction
- Form handling
- Dashboard visualizations
- Communication with the backend API

---

## Backend Architecture

The backend is built using **Java and Spring Boot**. It exposes a REST API consumed by the frontend and follows a **layered architecture**.

### Technologies

| Technology        | Purpose                   |
| ----------------- | ------------------------- |
| Java              | Primary language           |
| Spring Boot       | Application framework      |
| Spring Web        | REST API layer             |
| Spring Data JPA   | Data access abstraction    |
| Hibernate         | ORM                        |
| MySQL             | Relational database        |
| Swagger / OpenAPI | API documentation          |

### Directory Structure

```
server/src/main/java/com/adnest/
├── controller/
├── service/
├── repository/
├── entity/
├── dto/
└── config/
```

### Layers

#### Controller

Handles incoming HTTP requests and maps API endpoints.

#### Service

Contains business logic. Processes financial data such as expenses, savings, and budgets.

#### Repository

Handles database communication using Spring Data JPA.

#### Entity

Defines the database models:

- `User`
- `Expense`
- `Category`
- `SavingsGoal`
- `Budget`

---

## API Communication

Frontend and backend communicate through REST endpoints. All API responses are in **JSON format**.

### Example Endpoints

```http
GET  /api/expenses
POST /api/expenses

GET  /api/goals
POST /api/goals

GET  /api/budgets
```

---

## API Documentation

The backend includes **Swagger / OpenAPI**, which provides an interactive interface for browsing and testing API endpoints.

```
http://localhost:8080/swagger-ui.html
```

---

## Database

The system uses **MySQL** as its relational database.

### Responsibilities

- Store financial data
- Maintain user records
- Store savings goals
- Manage budgets
- Track expenses

---

## Security

Authentication is required to access the API.

Users are predefined:

| Username | Role  |
| -------- | ----- |
| Alan     | User  |
| Dennise  | User  |

> User registration is disabled. New accounts must be created manually.

---

## Development Philosophy

The system prioritizes:

- **Clean architecture** — clear separation of concerns between layers
- **Maintainable code** — readable and consistent style throughout
- **Simplicity** — avoid over-engineering; solve the actual problem
- **Clarity** — financial information must be easy to understand at a glance

The goal is to build a reliable and simple financial management tool for two users.