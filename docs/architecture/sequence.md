# UML Sequence Diagram for the Budget Tracker: Log a Purchase

```mermaid
sequenceDiagram
  autonumber
  actor S as Student
  participant UI as Log Purchase Page (Next.js)
  participant API as /api/expenses (Route Handler)
  participant DB as Database
  participant NS as Notification Service
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
    API->>API: recalculate remaining balance and pace
    alt spending ahead of pace
      API->>DB: insert alert (status = PENDING)
      API->>NS: request alert delivery
      NS-->>API: accepted
      API->>DB: set alert status = SENT
      API-->>UI: 201 Created {expenseId, remainingBalance, aheadOfPace true}
      NS--)S: pace alert (email or push)
    else on pace
      API-->>UI: 201 Created {expenseId, remainingBalance, aheadOfPace false}
    end
    UI-->>S: show updated balance
  end
```

## Key

| Notation | Meaning |
|---|---|
| Solid arrow | Synchronous call (the caller waits) |
| Dashed arrow | Reply |
| Open-arrowhead arrow (`--)`) | Asynchronous message (alert delivered later) |
| alt / else box | Alternative paths, each with a guard |

## Notes

- This is the riskiest flow: it touches login, money-like data, an external system and a pace rule, and it is tied to the 5-second logging goal.
- The student's alert arrives asynchronously, after the API has already replied.
- The only web-to-API message is `POST /api/expenses`, which must appear in the API contract.
- Not drawn: 400 (invalid input) and 401 (not logged in) responses.
