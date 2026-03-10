# ADNest — Use Cases

## Overview

This document defines the functional behavior of ADNest.

The goal of the system is to provide a **simple and intuitive financial management tool for two users**:

* Alan
* Dennise

The system allows both users to:

* record expenses
* track shared spending
* create savings goals
* manage budgets
* view financial insights through charts

The application should remain **simple, fast, and intuitive**.

---

# Primary Actors

The system has only one actor type:

### User

Users are predefined in the database.

```
Alan
Dennise
```

Both users interact with the same shared financial system.

---

# Core Use Cases

The following use cases describe the main interactions supported by ADNest.

---

# UC-01 — Login

### Description

Allows a predefined user to authenticate into the system.

### Flow

1. User opens the login page
2. User enters email and password
3. Backend validates credentials
4. User is granted access to the dashboard

### Result

User gains access to the application.

---

# UC-02 — Create Expense

### Description

Allows a user to record a new expense.

### Flow

1. User opens the expense form
2. User enters:

* title
* amount
* category
* account type
* date
* notes
* shared (true/false)

3. User submits the form
4. Backend stores the expense

### Result

The expense is stored and becomes visible in the system.

---

# UC-03 — View Expenses

### Description

Allows users to see a list of recorded expenses.

### Flow

1. User opens the expenses page
2. System loads expenses from the API
3. Expenses are displayed in a list

Displayed information:

* title
* amount
* category
* date
* createdBy
* shared

### Result

User can review financial activity.

---

# UC-04 — Create Category

### Description

Allows users to define custom spending categories.

### Flow

1. User opens category settings
2. User enters category name
3. User selects color
4. Category is saved

### Result

Category becomes available when creating expenses.

---

# UC-05 — Create Savings Goal

### Description

Allows users to create a shared savings goal.

### Flow

1. User opens savings goals page
2. User creates a new goal
3. User enters:

* name
* target amount
* deadline
* description

4. Backend stores the goal

### Result

Goal appears in the savings goals list.

---

# UC-06 — Contribute to Savings Goal

### Description

Allows users to add money toward a savings goal.

### Flow

1. User selects a savings goal
2. User enters contribution amount
3. Backend records the contribution
4. Goal progress is recalculated

### Result

Savings progress increases.

---

# UC-07 — Create Budget

### Description

Allows users to define spending limits.

Two types of budgets are supported:

* global monthly budget
* category budget

### Flow

1. User opens budget page
2. User creates a budget
3. User enters:

* category (optional)
* limit amount
* month
* year

### Result

Budget becomes active.

---

# UC-08 — View Dashboard

### Description

Provides a financial overview through charts.

### Dashboard Data

The dashboard displays:

* total monthly spending
* spending by category
* personal vs shared expenses

### Flow

1. User opens dashboard
2. Frontend requests analytics data
3. Backend calculates statistics
4. Charts are displayed

---

# UC-09 — Manage Recurring Expenses

### Description

Allows users to define expenses that occur automatically.

Examples:

```
Netflix
Spotify
Gym
Internet
```

### Flow

1. User creates recurring expense
2. User defines:

* title
* amount
* category
* payment method
* frequency

3. System stores recurring expense

### Result

Recurring expenses are used to automatically generate future expenses.

---

# System Simplicity Principles

ADNest is intentionally designed to remain simple.

The system should prioritize:

* fast expense entry
* clear financial visibility
* minimal configuration
* intuitive UI

The goal is to provide a **clean financial dashboard for a couple managing their money together**.

---

# Backend Implementation Pattern

The backend should follow a simple layered architecture.

```
Controller
Service
Repository
Entity
DTO
```

Responsibilities:

Controller
Handles HTTP requests.

Service
Contains business logic.

Repository
Handles database operations.

Entity
Represents database models.

DTO
Defines API responses.

---

# Frontend Interaction Model

The frontend communicates with the backend using **simple REST requests**.

Example:

```
GET /api/expenses
POST /api/expenses
GET /api/categories
POST /api/categories
GET /api/goals
POST /api/goals
```

Requests should be performed using **fetch**.

Example:

```javascript
const res = await fetch("/api/expenses");
const data = await res.json();
```

The frontend should remain lightweight and focused on:

* displaying data
* submitting forms
* rendering charts
