# Entity-Relationship Diagram (Draft) for the Budget Tracker

```mermaid
erDiagram
  USERS ||--o{ ALLOWANCE_PERIODS : sets
  ALLOWANCE_PERIODS ||--o{ EXPENSES : contains
  ALLOWANCE_PERIODS ||--o{ ALERTS : triggers
  USERS {
    uuid id PK
    text name "PII"
    text email "PII"
    text password_hash "sensitive"
    timestamp created_at
  }
  ALLOWANCE_PERIODS {
    uuid id PK
    uuid user_id FK
    numeric amount "personal financial data"
    text period_type "WEEKLY or MONTHLY"
    date start_date
    date end_date
    text status "SCHEDULED, ACTIVE or CLOSED"
  }
  EXPENSES {
    uuid id PK
    uuid period_id FK
    numeric amount "personal financial data"
    text note "may contain personal info"
    timestamp spent_at
    timestamp created_at
  }
  ALERTS {
    uuid id PK
    uuid period_id FK
    text message
    text status "PENDING, SENT or FAILED"
    timestamp created_at
    timestamp sent_at
  }
```

## Key

| Symbol | Meaning |
|---|---|
| `\|\|` | Exactly one |
| `o{` | Zero or more |
| PK / FK | Primary key / foreign key |
| "PII" and similar comments | Personal or sensitive data to protect |

## Notes

- Derived from `class.md`: one table per stored class. The three enumerations are stored as text columns with the same values.
- The 1-to-many multiplicities in the class diagram become the foreign keys `user_id` and `period_id`.
- Draft: finalized with the database schema in Week 9.
