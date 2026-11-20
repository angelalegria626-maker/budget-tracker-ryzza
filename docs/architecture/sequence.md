# UML Sequence Diagrams for the Budget Tracker

## Scenario 1: Log a purchase

```mermaid
sequenceDiagram
  autonumber
  actor Student
  participant Page as Log Purchase Page (Next.js)
  participant API as /api/expenses (Route Handler)
  participant DB as Database

  Student->>Page: enter amount and note, tap Save
  Page->>API: POST /api/expenses [amount, note, spentAt]
  API->>API: check session and validate input
  API->>DB: find active allowance period
  DB-->>API: period or none
  alt no active allowance period
    API-->>Page: 409 Conflict [code NO_ACTIVE_PERIOD]
    Page-->>Student: ask student to set an allowance
  else active period found
    API->>API: assign category from note
    API->>DB: insert expense [with category]
    DB-->>API: expenseId
    API->>DB: sum expenses in the period
    DB-->>API: total spent
    API->>API: calculate remaining balance, pace and runway days
    alt spending ahead of pace
      API->>DB: insert pace alert [status = UNREAD]
      DB-->>API: alertId
      API-->>Page: 201 Created [expenseId, category, remainingBalance, runwayDays, aheadOfPace true]
      Page-->>Student: show balance, runway and pace alert
    else on pace
      API-->>Page: 201 Created [expenseId, category, remainingBalance, runwayDays, aheadOfPace false]
      Page-->>Student: show updated balance and runway
    end
  end
```

## Scenario 2: Add to a savings goal

```mermaid
sequenceDiagram
  autonumber
  actor Student
  participant Page as Savings Goal Page (Next.js)
  participant API as /api/savings-goals (Route Handler)
  participant DB as Database

  Student->>Page: enter amount to add, tap Save
  Page->>API: PATCH /api/savings-goals [goalId, addAmount]
  API->>API: check session and validate input
  API->>DB: find savings goal of this student
  DB-->>API: goal or none
  alt goal not found
    API-->>Page: 404 Not Found
    Page-->>Student: ask student to set a savings goal
  else goal found
    API->>DB: update savedAmount
    DB-->>API: updated goal
    API->>API: calculate progress percent and amount still needed
    API-->>Page: 200 OK [savedAmount, progressPercent, remainingNeeded]
    Page-->>Student: show progress and amount still needed
  end
```

## Notes

- **Audience / risk:** developers; it fixes the order of messages and the response codes before the front end is built.
- Scenario 1 is the same "log a purchase" flow as before, with two additions: the API assigns a category when it inserts the expense, and the response now includes the category and runway days.
- One round trip returns the balance, runway and alert together, which keeps logging under 5 seconds.
- Scenario 2 is new. Setting the goal itself (POST /api/savings-goals) is a simple insert and is not drawn separately.
