# Entity-Relationship Diagram (Draft) for the Budget Tracker

```mermaid
erDiagram
  STUDENTS ||--o{ ALLOWANCE_PERIODS : sets
  ALLOWANCE_PERIODS ||--o{ EXPENSES : contains
  ALLOWANCE_PERIODS ||--o{ PACE_ALERTS : triggers
  STUDENTS {
    uuid id PK
    text name "PII"
    text email "PII"
    text password_hash "sensitive"
    timestamp created_at
  }
  ALLOWANCE_PERIODS {
    uuid id PK
    uuid student_id FK
    decimal amount "personal financial data"
    text period_type "WEEKLY or MONTHLY"
    date start_date
    date end_date
    text status "ACTIVE or CLOSED"
  }
  EXPENSES {
    uuid id PK
    uuid period_id FK
    decimal amount "personal financial data"
    text note "may contain personal info"
    timestamp spent_at
    timestamp created_at
  }
  PACE_ALERTS {
    uuid id PK
    uuid period_id FK
    text message
    text status "UNREAD or DISMISSED"
    timestamp created_at
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

- **Audience / risk:** developers and whoever protects the data; it reduces the risk of a wrong schema and of leaking personal data.
- Derived from `class.md`: one table per stored class. The three enumerations are stored as text columns with the same values.
- The 1-to-many multiplicities in the class diagram become the foreign keys `student_id` and `period_id`.
- Remaining balance is not stored; it is calculated from `amount` and the expenses.
- The ERD uses snake_case and the class diagram uses camelCase. This is a naming convention, not a mismatch.
- Draft: finalized with the database schema later.
