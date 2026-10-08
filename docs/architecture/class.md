# UML Class Diagram for the Budget Tracker Domain

```mermaid
classDiagram
  direction LR
  class User {
    +id: string
    +name: string
    +email: string
    -passwordHash: string
    +createdAt: DateTime
    +login() bool
  }
  class AllowancePeriod {
    +id: string
    +amount: number
    +periodType: PeriodType
    +startDate: Date
    +endDate: Date
    +status: PeriodStatus
    +remainingBalance() number
    +isAheadOfPace() bool
    +close()
  }
  class Expense {
    +id: string
    +amount: number
    +note: string
    +spentAt: DateTime
    +createdAt: DateTime
  }
  class Alert {
    +id: string
    +message: string
    +status: AlertStatus
    +createdAt: DateTime
    +sentAt: DateTime
  }
  class PeriodType {
    <<enumeration>>
    WEEKLY
    MONTHLY
  }
  class PeriodStatus {
    <<enumeration>>
    SCHEDULED
    ACTIVE
    CLOSED
  }
  class AlertStatus {
    <<enumeration>>
    PENDING
    SENT
    FAILED
  }
  User "1" --> "0..*" AllowancePeriod : sets
  AllowancePeriod "1" *-- "0..*" Expense : contains
  AllowancePeriod "1" --> "0..*" Alert : triggers
  AllowancePeriod ..> PeriodType : uses
  AllowancePeriod ..> PeriodStatus : uses
  Alert ..> AlertStatus : uses
```

## Key

| Notation | Meaning |
|---|---|
| Box with three parts | Class: name, attributes, operations |
| Solid arrow with label | Association, with multiplicity at both ends |
| Filled diamond | Composition: an Expense cannot exist without its AllowancePeriod |
| Dashed arrow | A class uses an enumeration |
| «enumeration» | A fixed list of allowed values |

## Notes

- `PeriodStatus` values match the state machine in `state-machine.md`.
- `createdAt` on every logged purchase supports the activation, retention and under-5-seconds metrics from the Lean Canvas.
- `passwordHash` is private and never leaves the server.
