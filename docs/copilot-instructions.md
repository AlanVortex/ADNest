# Copilot Development Instructions — ADNest

You are assisting in building the backend and frontend for a financial management system called **ADNest**.

Before generating code, read all documentation inside the `docs/` folder.

Important files:

* 00-system-overview.md
* 01-system-architecture.md
* 02-domain-model.md
* 03-use-cases.md
* 04-api-design.md

These documents define the system requirements and architecture.

Always follow them as the **source of truth**.

---

# Backend Requirements

The backend must be implemented using:

* Java
* Spring Boot
* Spring Web
* Spring Data JPA
* MySQL
* Swagger (Springdoc OpenAPI)
* Lombok

Architecture pattern:

```
Controller
Service
Repository
Entity
DTO
```

Rules:

* Controllers handle HTTP requests
* Services contain business logic
* Repositories handle database access
* Entities represent database tables
* DTOs define API responses

Do not place business logic in controllers.

---

# Entities to Implement

Entities are defined in `02-domain-model.md`.

Main entities:

* User
* Category
* Expense
* AccountType
* SavingsGoal
* SavingsContribution
* Budget
* RecurringExpense

Use JPA annotations.

---

# API Endpoints

Endpoints are defined in `04-api-design.md`.

Examples:

```
GET /api/expenses
POST /api/expenses

GET /api/categories
POST /api/categories

GET /api/goals
POST /api/goals
```

Controllers must follow REST best practices.

---

# Database

Use MySQL with JPA/Hibernate.

Money fields must use:

```
DECIMAL(12,2)
```

Relationships must follow the domain model.

---

# Swagger

Swagger documentation must be enabled using Springdoc OpenAPI.

Swagger UI must be available at:

```
/swagger-ui.html
```

---

# Frontend Requirements

Frontend is built with:

* Astro
* React
* TypeScript
* TailwindCSS

Frontend communicates with the backend using REST.

Example:

```javascript
const res = await fetch("/api/expenses")
```

Frontend responsibilities:

* display dashboard
* create expenses
* create savings goals
* show analytics charts

---

# Development Philosophy

The system must remain simple and intuitive.

This application is designed for **two users managing their finances together**.

Priorities:

* simple UI
* fast expense creation
* clear financial analytics
* maintainable backend code

Always generate clean and readable code.
