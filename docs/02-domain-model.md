# ADNest — Domain Model

## Domain Overview

ADNest is a simple financial management system designed for **two users sharing a single financial space**.

The system allows both users to:

* track expenses
* manage savings goals
* define budgets
* visualize spending analytics

All financial values are stored in **MXN (Mexican Peso)**.

The system intentionally keeps the domain **simple and focused**.

---

# Core Domain Entities

The system contains the following entities:

* User
* AccountType
* Category
* Expense
* SavingsGoal
* SavingsContribution
* Budget
* RecurringExpense

---

# User

Represents a user of the system.

There are only **two predefined users**.

```
Alan
Dennise
```

Users share the same financial environment.

### Fields

| Field        | Type      | Description        |
| ------------ | --------- | ------------------ |
| id           | Long      | Unique identifier  |
| name         | String    | User name          |
| email        | String    | Login email        |
| passwordHash | String    | Encrypted password |
| createdAt    | Timestamp | Creation timestamp |

---

# AccountType

Represents the type of payment method used for an expense.

### Supported Types

```
CASH
DEBIT
CREDIT
```

### Fields

| Field | Type   | Description       |
| ----- | ------ | ----------------- |
| id    | Long   | Identifier        |
| name  | String | Account type name |

---

# Category

Represents a spending category.

Categories are **user-defined**.

Examples:

```
Food
Transport
Shopping
Subscriptions
Entertainment
```

### Fields

| Field     | Type      | Description        |
| --------- | --------- | ------------------ |
| id        | Long      | Identifier         |
| name      | String    | Category name      |
| color     | String    | Color used in UI   |
| createdAt | Timestamp | Creation timestamp |

---

# Expense

Represents a financial expense.

### Fields

| Field         | Type        | Description                  |
| ------------- | ----------- | ---------------------------- |
| id            | Long        | Identifier                   |
| title         | String      | Expense title                |
| amount        | Decimal     | Expense amount               |
| categoryId    | Category    | Expense category             |
| accountTypeId | AccountType | Payment method               |
| createdBy     | User        | User who created the expense |
| shared        | Boolean     | Indicates shared expense     |
| date          | Date        | Expense date                 |
| notes         | String      | Optional notes               |

### Shared Expense Rule

If `shared = true`, the expense is split **50/50** between both users.

---

# SavingsGoal

Represents a shared savings objective.

Examples:

```
Vacation
Emergency Fund
Laptop
```

### Fields

| Field        | Type      | Description        |
| ------------ | --------- | ------------------ |
| id           | Long      | Identifier         |
| name         | String    | Goal name          |
| targetAmount | Decimal   | Target savings     |
| deadline     | Date      | Optional deadline  |
| description  | String    | Goal description   |
| createdAt    | Timestamp | Creation timestamp |

### Progress Calculation

The progress of a goal is calculated using contributions.

---

# SavingsContribution

Represents a deposit toward a savings goal.

Both users can contribute.

### Fields

| Field  | Type        | Description         |
| ------ | ----------- | ------------------- |
| id     | Long        | Identifier          |
| goalId | SavingsGoal | Related goal        |
| userId | User        | Contributor         |
| amount | Decimal     | Contribution amount |
| date   | Date        | Contribution date   |

---

# Budget

Budgets define spending limits.

The system supports:

1️⃣ Monthly global budget
2️⃣ Category budgets

### Fields

| Field       | Type     | Description       |
| ----------- | -------- | ----------------- |
| id          | Long     | Identifier        |
| categoryId  | Category | Optional category |
| limitAmount | Decimal  | Budget limit      |
| month       | Integer  | Month             |
| year        | Integer  | Year              |

If `categoryId` is null → global monthly budget.

---

# RecurringExpense

Represents an expense that repeats automatically.

Examples:

```
Netflix
Spotify
Gym
Internet
```

### Fields

| Field             | Type        | Description      |
| ----------------- | ----------- | ---------------- |
| id                | Long        | Identifier       |
| title             | String      | Expense title    |
| amount            | Decimal     | Amount           |
| categoryId        | Category    | Category         |
| accountTypeId     | AccountType | Payment method   |
| frequency         | Enum        | MONTHLY / WEEKLY |
| nextExecutionDate | Date        | Next occurrence  |

---

# Entity Relationships

```
User
 ├ creates → Expense
 └ contributes → SavingsContribution

Category
 ├ classifies → Expense
 └ classifies → RecurringExpense

AccountType
 └ used by → Expense

Expense
 └ belongs to → Category

SavingsGoal
 └ receives → SavingsContribution

Budget
 └ optionally belongs to → Category

RecurringExpense
 └ generates → Expense
```

---

# Domain Rules

The system enforces the following rules:

1. Only two predefined users exist.
2. Expenses must belong to a category.
3. Expenses must have a payment method.
4. Shared expenses are split 50/50.
5. Savings progress is calculated from contributions.
6. Budgets are evaluated monthly.
7. Recurring expenses generate automatic expenses.
