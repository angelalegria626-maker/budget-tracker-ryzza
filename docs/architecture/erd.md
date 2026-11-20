# Entity Relationship Diagram (Draft) for the Budget Tracker

```mermaid
erDiagram
  STUDENTS ||--o{ ALLOWANCE_PERIODS : sets
  STUDENTS ||--o{ SAVINGS_GOALS : "saves for"
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
    text category "MEALS, TRANSPORT, SNACKS, SCHOOL or OTHER"
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
  SAVINGS_GOALS {
    uuid id PK
    uuid student_id FK
    text name
    decimal target_amount "personal financial data"
    decimal saved_amount "personal financial data"
    timestamp created_at
  }
```

## Key

| Notation | Meaning |
|---|---|
| PK / FK | Primary key / foreign key |
| `\|\|--o{` | One to many |
| Quoted text | Privacy or value notes on a field |

## Notes

- **Audience / risk:** developers and privacy reviewers; it flags where personal and financial data is stored.
- **New in this version:** a category column on EXPENSES and a new SAVINGS_GOALS table linked to STUDENTS.
- Runway days and progress percent are calculated, not stored, so they do not appear as columns.
- name and email are PII, password_hash is sensitive, and the amount fields hold personal financial data.
