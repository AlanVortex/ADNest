# ADNest — Domain Model

## Domain Overview

ADNest is a financial management system designed for **two predefined users**.

The domain model represents the core financial entities required to manage:

* personal expenses
* shared expenses
* savings goals
* budgets
* financial analytics

The system follows a **domain-driven structure** where financial data is represented through clearly defined entities and relationships.

All financial values are stored using **MXN (Mexican Peso)**.

---

# Core Domain Entities

The system is composed of the following primary entities:

* User
* Account
* Category
* Expense
* SavingsGoal
* SavingsContribution
* Budget

Each entity represents a financial concept used by the system.

---

# User

Represents a person who uses the system.

The system only supports two predefined users:

* Alan
* Dennise

Users are seeded directly into the database.

### Fields

```
User
```

| Field        | Type        | Description        |
| ------------ | ----------- | ------------------ |
| id           | UUID / Long | Unique identifier  |
| name         | String      | User display name  |
| email        | String      | Login identifier   |
| passwordHash | String      | Encrypted password |
| createdAt    | Timestamp   | User creation date |

### Notes

* Registration is disabled.
* Users are predefined.
* Authentication will use stored credentials.

---

# Account

Represents a financial source used to pay for expenses.

Supported account types:

* Cash
* Debit Card
* Credit Card

### Fields

```
Account
```

| Field   | Type        | Description           |
| ------- | ----------- | --------------------- |
| id      | UUID / Long | Unique identifier     |
| name    | String      | Account name          |
| type    | Enum        | CASH / DEBIT / CREDIT |
| ownerId | User        | Owner of the account  |

### Notes

Accounts allow the system to track **where money comes from**.

Example:

Alan's Debit Card
Dennise's Credit Card
Shared Cash

---

# Category

Represents a spending category.

Examples:

* Food
* Transport
* Entertainment
* Subscriptions
* Shopping

### Fields

```
Category
```

| Field     | Type        | Description             |
| --------- | ----------- | ----------------------- |
| id        | UUID / Long | Unique identifier       |
| name      | String      | Category name           |
| color     | String      | UI color representation |
| createdAt | Timestamp   | Creation date           |

### Notes

Categories help analyze spending patterns.

---

# Expense

Represents a financial transaction where money is spent.

Expenses may be:

* personal
* shared

### Fields

```
Expense
```

| Field      | Type        | Description                   |
| ---------- | ----------- | ----------------------------- |
| id         | UUID / Long | Unique identifier             |
| title      | String      | Expense description           |
| amount     | Decimal     | Expense amount                |
| categoryId | Category    | Spending category             |
| accountId  | Account     | Payment source                |
| createdBy  | User        | User who recorded the expense |
| isShared   | Boolean     | Indicates shared expense      |
| date       | Date        | Expense date                  |
| notes      | String      | Optional description          |

### Notes

Shared expenses affect both users.

Personal expenses affect only the owner.

---

# SavingsGoal

Represents a financial objective where users accumulate money over time.

Examples:

* vacation
* emergency fund
* new laptop
* car

### Fields

```
SavingsGoal
```

| Field         | Type        | Description          |
| ------------- | ----------- | -------------------- |
| id            | UUID / Long | Unique identifier    |
| name          | String      | Goal name            |
| targetAmount  | Decimal     | Target amount        |
| currentAmount | Decimal     | Current saved amount |
| deadline      | Date        | Optional deadline    |
| createdAt     | Timestamp   | Creation date        |

### Notes

Savings goals are shared between both users.

---

# SavingsContribution

Represents a deposit toward a savings goal.

Both users can contribute.

### Fields

```
SavingsContribution
```

| Field  | Type        | Description          |
| ------ | ----------- | -------------------- |
| id     | UUID / Long | Unique identifier    |
| goalId | SavingsGoal | Related savings goal |
| userId | User        | Contributor          |
| amount | Decimal     | Contribution amount  |
| date   | Date        | Contribution date    |

### Notes

The system updates the goal's `currentAmount` automatically.

---

# Budget

Represents a monthly spending limit for a category.

### Fields

```
Budget
```

| Field       | Type        | Description              |
| ----------- | ----------- | ------------------------ |
| id          | UUID / Long | Unique identifier        |
| categoryId  | Category    | Budget category          |
| limitAmount | Decimal     | Maximum allowed spending |
| month       | Integer     | Month (1–12)             |
| year        | Integer     | Budget year              |

### Notes

Budgets allow users to monitor spending limits.

The system calculates:

* current spending
* remaining budget

---

# Entity Relationships

The system relationships are defined as follows:

```
User
 ├── owns → Account
 ├── creates → Expense
 └── contributes → SavingsContribution

Account
 └── used by → Expense

Category
 └── classifies → Expense

Expense
 └── belongs to → Category
 └── paid from → Account

SavingsGoal
 └── receives → SavingsContribution

SavingsContribution
 └── belongs to → SavingsGoal

Budget
 └── belongs to → Category
```

---

# Domain Rules

The system must enforce the following rules:

1. Only predefined users exist.
2. Expenses must belong to a category.
3. Expenses must belong to an account.
4. Shared expenses affect both users.
5. Savings contributions increase goal progress.
6. Budgets are evaluated per month and category.

---

# Financial Precision

All financial values must use **decimal types** to avoid floating-point errors.

Recommended database type:

```
DECIMAL(12,2)
```

---

# Future Domain Extensions

Potential future domain extensions may include:

* recurring expenses
* subscriptions
* debt tracking
* bank imports
* financial reports
