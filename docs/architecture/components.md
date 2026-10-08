# UML Component Diagram for the Budget Tracker API Application

```mermaid
flowchart LR
  WEB["«component»<br/>Web Application<br/>(caller)"]
  I1(("IExpenses"))
  I2(("IAllowance"))
  I3(("IAuth"))
  ES["«component»<br/>Expense Service"]
  AS["«component»<br/>Allowance Service"]
  AG["«component»<br/>Auth Guard"]
  I4(("IPace"))
  PC["«component»<br/>Pace Calculator"]
  I5(("IBudgetStore"))
  REPO["«component»<br/>Budget Repository"]
  DBX[("«database»<br/>Relational database")]
  WEB -- requires --> I1
  WEB -- requires --> I2
  WEB -- requires --> I3
  I1 --- ES
  I2 --- AS
  I3 --- AG
  ES -- requires --> I4
  ES -- requires --> I5
  AS -- requires --> I5
  AG -- requires --> I5
  I4 --- PC
  I5 --- REPO
  REPO -- SQL --> DBX
```

## Key

| Notation | Meaning |
|---|---|
| «component» box | A replaceable part with a clear responsibility |
| Circle | An interface (a service offered or needed) |
| Line from a circle to a component | The component provides that interface |
| "requires" arrow | The component needs that interface |

## Notes

- **Audience / risk:** developers; it reduces the risk of tight coupling between logic and storage.
- Budget Repository is the only component that runs SQL.
- Auth Guard checks the session before any expense or allowance logic runs.
- The MVP has no external services (no bank linking, no payments). If one is added later, it goes behind its own adapter interface.
