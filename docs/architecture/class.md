# UML Class Diagram for the Budget Tracker (Domain Model)

```mermaid
classDiagram
  class Student {
    +String id
    +String name
    +String email
    -String passwordHash
    +DateTime createdAt
  }
  class AllowancePeriod {
    +String id
    +Decimal amount
    +PeriodType periodType
    +Date startDate
    +Date endDate
    +PeriodStatus status
    +remainingBalance() Decimal
    +isAheadOfPace() Boolean
    +runwayDays() Integer
    +close() void
  }
  class Expense {
    +String id
    +Decimal amount
    +String note
    +Category category
    +DateTime spentAt
    +DateTime createdAt
  }
  class PaceAlert {
    +String id
    +String message
    +AlertStatus status
    +DateTime createdAt
  }
  class SavingsGoal {
    +String id
    +String name
    +Decimal targetAmount
    +Decimal savedAmount
    +DateTime createdAt
    +addSavings(amount) void
    +remainingNeeded() Decimal
    +progressPercent() Decimal
  }
  class PeriodType {
    <<enumeration>>
    WEEKLY
    MONTHLY
  }
  class PeriodStatus {
    <<enumeration>>
    ACTIVE
    CLOSED
  }
  class AlertStatus {
    <<enumeration>>
    UNREAD
    DISMISSED
  }
  class Category {
    <<enumeration>>
    MEALS
    TRANSPORT
    SNACKS
    SCHOOL
    OTHER
  }

  Student "1" --> "0..*" AllowancePeriod : sets
  Student "1" --> "0..*" SavingsGoal : saves for
  AllowancePeriod "1" *-- "0..*" Expense : contains
  AllowancePeriod "1" --> "0..*" PaceAlert : triggers
  AllowancePeriod ..> PeriodType : uses
  AllowancePeriod ..> PeriodStatus : uses
  PaceAlert ..> AlertStatus : uses
  Expense ..> Category : uses
```

## Key

| Notation | Meaning |
|---|---|
| `+` | Public attribute or method |
| `-` | Private attribute (passwordHash) |
| Filled diamond | Composition: expenses belong to their period |
| Arrow | Association |
| Dotted arrow | Uses an enumeration |

## Notes

- **Audience / risk:** developers; it keeps the domain model, the API and the database consistent.
- AllowancePeriod holds the key behaviour: remainingBalance(), isAheadOfPace(), runwayDays() and close().
- **New in this version:** a Category enumeration on Expense, a runwayDays() method on AllowancePeriod, and a SavingsGoal class owned by the Student.
- A savings goal belongs to the Student, not to one allowance period, because a goal can last longer than a week.
- PeriodType still allows MONTHLY. Remove it if the MVP targets weekly allowance only.
