# ADNest — System Overview

## Project Summary

ADNest is a private financial management system designed exclusively for two users: **Alan and Dennise**.

The purpose of the system is to help both users track personal and shared finances, manage expenses, create savings goals, and monitor budgets in a simple and clear way.

This application is not intended to be a public platform or multi-tenant system.  
It is a **closed system designed specifically for a couple**.

The system will provide a unified dashboard where both users can:

- Track personal expenses
- Track shared expenses
- Manage savings goals together
- Set monthly budgets
- Visualize financial insights through simple analytics

The main currency used in the system will be **MXN (Mexican Peso)**.

---

# Core Objectives

The application must allow Alan and Dennise to:

1. Track personal expenses independently
2. Record shared expenses between both users
3. Create and manage savings goals
4. Set monthly spending budgets
5. Monitor financial progress
6. Visualize spending patterns through analytics

The focus of the application is **clarity, simplicity, and usefulness for daily financial decisions**.

---

# System Scope

This system is intentionally limited to **two predefined users**.

Users will be **seeded directly in the database**:

- Alan
- Dennise

Authentication will still exist for security purposes, but **user registration is not required**, since the system is private.

---

# Supported Financial Sources

The system must support tracking expenses coming from different types of financial sources.

Supported account types:

- Cash (Efectivo)
- Debit Card (Tarjeta de débito)
- Credit Card (Tarjeta de crédito)

Each expense recorded in the system must indicate which source was used.

---

# Expense Types

The system will support two types of expenses:

### Personal Expenses

Expenses made by one user that affect only their personal finances.

Example:

Alan buys lunch.

### Shared Expenses

Expenses that affect both users.

Example:

Dinner together, groceries, subscriptions.

Shared expenses can be split between users.

---

# Savings Goals

The system must allow both users to create **savings goals**.

Examples of savings goals:

- Vacations
- Electronics
- Emergency fund
- Car
- Personal projects

Goals must contain:

- goal name
- target amount
- current saved amount
- deadline (optional)

Both users can contribute to the same goal.

---

# Budgets

The system must support **monthly budgets**.

Budgets allow users to define how much money can be spent in specific categories.

Examples:

Food  
Transport  
Entertainment

The system must show:

- total budget
- current spending
- remaining budget

---

# Analytics Dashboard

The application must provide a simple dashboard showing essential financial insights.

Examples of analytics:

- Monthly spending
- Spending by category
- Savings progress
- Personal vs shared expenses

The goal is to provide **clear financial visibility without overwhelming complexity**.

---

# Security Model

The system will support authentication to protect financial data.

Users:

- Alan
- Dennise

Credentials will be stored securely in the database.

Registration is disabled because users are predefined.

---

# Technology Stack

Frontend

- Astro
- React
- TypeScript
- TailwindCSS
- Vite

Backend

- Java
- Spring Boot
- Spring Web
- Spring Data JPA
- Swagger / OpenAPI

Database

- MySQL

---

# Design Philosophy

ADNest should follow these principles:

- Simplicity first
- Clear financial visualization
- Minimal friction when recording expenses
- Private and secure data
- Built specifically for two users

The goal is to create a **lightweight but powerful personal finance system**.

---

# Future Possibilities

Although the system is intentionally simple, future enhancements could include:

- recurring expenses
- export financial reports
- notifications for budget limits
- mobile version
- bank statement import

These features are **out of scope for the initial version**.