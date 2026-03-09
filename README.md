# ADNest

ADNest is a private financial management system designed exclusively for **two predefined users: Alan and Dennise**.

The application helps a couple manage their finances together by tracking expenses, organizing savings goals, managing budgets, and understanding spending habits through a simple and secure dashboard.

The name **ADNest** comes from the initials **A + D**, representing a shared financial space where both users build and manage their financial future.

This project is not intended to be a public financial platform.
It is a **private system built specifically for two users**.

---

# Purpose

ADNest is designed to help **Alan and Dennise**:

* track personal expenses
* track shared expenses
* create and monitor savings goals
* manage monthly budgets
* visualize financial progress

The goal is to provide a **clear, simple, and private financial overview** that helps both users make better financial decisions together.

---

# Users

The system supports **two predefined users only**.

These users will be seeded directly in the database:

* **Alan**
* **Dennise**

User registration is intentionally disabled because the system is private.

Authentication will still be implemented to protect financial data.

---

# Repository Structure

This project follows a **monorepo structure**.

```
ADNest
│
├ client
│   → Frontend application (Astro + React)
│
├ server
│   → Backend API (Spring Boot)
│
├ docs
│   → System documentation and architecture
│
└ README.md
```

---

# Tech Stack

## Frontend

* Astro
* React
* TypeScript
* TailwindCSS
* Vite

The frontend is responsible for:

* UI rendering
* dashboard visualization
* user interaction
* API communication

---

## Backend

* Java
* Spring Boot
* Spring Web
* Spring Data JPA
* Swagger / OpenAPI

The backend is responsible for:

* business logic
* financial data management
* authentication
* REST API endpoints

Swagger will provide interactive API documentation for development and testing.

---

## Database

* MySQL

The database will store:

* users
* expenses
* categories
* savings goals
* contributions
* budgets

---

# Core Features (Planned)

## Expense Tracking

Users can record:

* personal expenses
* shared expenses
* categorized spending

Supported financial sources include:

* cash
* debit card
* credit card

---

## Savings Goals

Users can create shared savings goals such as:

* vacations
* emergency funds
* large purchases

Each goal will include:

* goal name
* target amount
* current saved amount
* optional deadline

Both users can contribute to the same goal.

---

## Budget Management

Users can define monthly budgets for spending categories such as:

* food
* transportation
* entertainment
* subscriptions

The system will display:

* total budget
* current spending
* remaining amount

---

## Financial Dashboard

The dashboard will provide:

* monthly expense overview
* spending by category
* savings progress
* recent transactions

The goal is to provide **clear financial insights without unnecessary complexity**.

---

# API Documentation

The backend will include **Swagger / OpenAPI** documentation.

During development, API endpoints can be explored at:

```
http://localhost:8080/swagger-ui.html
```

---

# Development Status

ADNest is currently in **early development**.

The project is being built incrementally with the following phases:

1. System architecture and documentation
2. Frontend foundation (Astro + React)
3. Backend API (Spring Boot)
4. Database schema
5. Financial features implementation
6. Dashboard analytics

---

# License

Private project for personal use.
