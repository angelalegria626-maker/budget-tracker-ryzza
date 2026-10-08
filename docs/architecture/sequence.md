# UML Sequence Diagram for the Budget Tracker: Log a Purchase

```mermaid
sequenceDiagram
  autonumber
  actor S as Student
  participant UI as Log Purchase Page (Next.js)
  participant API as /api/expenses (Route Handler)
  participant DB as Database
  S->>UI: enter amount and note, tap Save
  UI->>API: POST /api/expenses {amount, note, spentAt}
  API->>API: check session and validate input
  API->>DB: find active allowance period
  DB-->>API: period or none
  alt no active allowance period
    API-->>UI: 409 Conflict {code NO_ACTIVE_PERIOD}
    UI-->>S: ask student to set an allowance
  else active period found
    API->>DB: insert expense
    DB-->>API: expenseId
    API->>DB: sum expenses in the period
    DB-->>API: total spent
    API->>API: calculate remaining balance and pace
    alt spending ahead of pace
      API->>DB: insert pace alert (status = UNREAD)
      DB-->>API: alertId
      API-->>UI: 201 Created {expenseId, remainingBalance, aheadOfPace true}
      UI-->>S: show balance and pace alert
    else on pace
      API-->>UI: 201 Created {expenseId, remainingBalance, aheadOfPace false}
      UI-->>S: show updated balance
    end
  end
```

## Key

| Notation | Meaning |
|---|---|
| Solid arrow | A call; the caller waits for the reply |
| Dashed arrow | A reply |
| alt / else box | Alternative paths, each with a condition |

## Notes

- **Audience / risk:** developers and testers; it reduces the risk of a slow or broken logging flow. This flow is the riskiest because the whole Lean Canvas depends on logging in under 5 seconds (our riskiest assumption, #2).
- It also changes data (a status-bearing PaceAlert is created) and depends on a signed-in student.
- There are no asynchronous messages and no external systems: the alert is returned in the same response and shown in the app.
- The only web-to-API message is `POST /api/expenses`, which must match the API contract.
- Not drawn: 400 (invalid input) and 401 (not signed in) responses.
