# ADNest — API Design

## Overview

This document defines the REST API used by the ADNest system.

The API is implemented using **Spring Boot** and exposes endpoints used by the Astro frontend.

All responses are returned in **JSON format**.

Base API path:

```
/api
```

---

# Authentication

Authentication is required to access protected endpoints.

Users are predefined in the database:

* Alan
* Dennise

## Login

```
POST /api/auth/login
```

### Request

```json
{
  "email": "alan@email.com",
  "password": "password"
}
```

### Response

```json
{
  "token": "jwt_token_here",
  "user": {
    "id": 1,
    "name": "Alan"
  }
}
```

---

# Categories

## Get Categories

```
GET /api/categories
```

### Response

```json
[
  {
    "id": 1,
    "name": "Food",
    "color": "#FFAA00"
  }
]
```

---

## Create Category

```
POST /api/categories
```

### Request

```json
{
  "name": "Transport",
  "color": "#00AAFF"
}
```

---

# Expenses

## Get All Expenses

```
GET /api/expenses
```

### Response

```json
[
  {
    "id": 1,
    "title": "Dinner",
    "amount": 450,
    "category": "Food",
    "accountType": "DEBIT",
    "shared": true,
    "createdBy": "Alan",
    "date": "2026-03-10"
  }
]
```

---

## Create Expense

```
POST /api/expenses
```

### Request

```json
{
  "title": "Groceries",
  "amount": 600,
  "categoryId": 1,
  "accountType": "DEBIT",
  "shared": true,
  "date": "2026-03-10",
  "notes": "Weekly groceries"
}
```

---

# Savings Goals

## Get Goals

```
GET /api/goals
```

---

## Create Goal

```
POST /api/goals
```

### Request

```json
{
  "name": "Vacation",
  "targetAmount": 15000,
  "deadline": "2026-12-01",
  "description": "Beach vacation"
}
```

---

# Savings Contributions

## Contribute to Goal

```
POST /api/goals/{goalId}/contribute
```

### Request

```json
{
  "amount": 500
}
```

---

# Budgets

## Get Budgets

```
GET /api/budgets
```

---

## Create Budget

```
POST /api/budgets
```

### Request

```json
{
  "categoryId": 1,
  "limitAmount": 4000,
  "month": 3,
  "year": 2026
}
```

If `categoryId` is null, the budget represents a **global monthly budget**.

---

# Recurring Expenses

## Get Recurring Expenses

```
GET /api/recurring-expenses
```

---

## Create Recurring Expense

```
POST /api/recurring-expenses
```

### Request

```json
{
  "title": "Netflix",
  "amount": 199,
  "categoryId": 5,
  "accountType": "CREDIT",
  "frequency": "MONTHLY"
}
```

---

# Analytics

## Dashboard Data

```
GET /api/analytics/dashboard
```

### Response

```json
{
  "monthlySpending": 8500,
  "spendingByCategory": [],
  "personalVsShared": []
}
```

This endpoint provides the data used by the frontend dashboard charts.

---

# API Principles

The API should follow these principles:

* RESTful endpoints
* clear naming conventions
* DTO-based responses
* service-layer business logic
* repository-layer data access
