# UML Component Diagram for the Budget Tracker

```mermaid
flowchart LR
  Web["«component»<br/>Web Application<br/>(caller)"]

  IExp(("IExpenses"))
  IAll(("IAllowance"))
  ISav(("ISavings"))
  IAuth(("IAuth"))
  IPace(("IPace"))
  ICat(("ICategorize"))
  IStore(("IBudgetStore"))

  Exp["«component»<br/>Expense Service"]
  All["«component»<br/>Allowance Service"]
  Sav["«component»<br/>Savings Service"]
  Auth["«component»<br/>Auth Guard"]
  Pace["«component»<br/>Pace and Runway Calculator"]
  Cls["«component»<br/>Category Classifier"]
  Repo["«component»<br/>Budget Repository"]
  DB[("«database»<br/>Relational database")]

  Web -->|requires| IExp
  Web -->|requires| IAll
  Web -->|requires| ISav
  Web -->|requires| IAuth

  IExp --- Exp
  IAll --- All
  ISav --- Sav
  IAuth --- Auth

  Exp -->|requires| IPace
  Exp -->|requires| ICat
  Exp -->|requires| IStore
  All -->|requires| IStore
  Sav -->|requires| IStore
  Auth -->|requires| IStore

  IPace --- Pace
  ICat --- Cls
  IStore --- Repo
  Repo -->|SQL| DB

  classDef comp fill:#ede9fe,stroke:#7c3aed,color:#000
  classDef iface fill:#e0e7ff,stroke:#6366f1,color:#000
  class Web,Exp,All,Sav,Auth,Pace,Cls,Repo comp
  class IExp,IAll,ISav,IAuth,IPace,ICat,IStore iface
```

## Key

| Notation | Meaning |
|---|---|
| Rectangle «component» | A logical part of the system |
| Circle | An interface (ball) that a component provides |
| `requires` arrow | The component on the left depends on that interface |

## Notes

- **Audience / risk:** developers; components depend on interfaces, not on each other, so one piece can change without breaking the rest.
- **New in this version:** Savings Service (ISavings), Category Classifier (ICategorize) and a Pace Calculator that now also computes runway days (IPace).
- The Expense Service uses ICategorize, so the keyword rules can be replaced later without touching the rest.
- All services reach the database only through IBudgetStore.
