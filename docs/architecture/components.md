# UML Component Diagram for the Budget Tracker API Application

```mermaid
flowchart LR
  WEB["«component»<br/>Web UI<br/>(caller, Next.js pages)"]
  I1(("IExpenses"))
  I2(("IAuth"))
  ES["«component»<br/>Expense Service"]
  AG["«component»<br/>Auth Guard"]
  I3(("IPace"))
  PC["«component»<br/>Pace Calculator"]
  I4(("INotifier"))
  NA["«component»<br/>Notification Adapter"]
  I5(("IBudgetStore"))
  REPO["«component»<br/>Budget Repository"]
  EXT["«external»<br/>Notification Service"]
  DBX[("«database»<br/>PostgreSQL")]
  WEB -- requires --> I1
  WEB -- requires --> I2
  I1 --- ES
  I2 --- AG
  ES -- requires --> I3
  ES -- requires --> I4
  ES -- requires --> I5
  I3 --- PC
  I4 --- NA
  I5 --- REPO
  NA -- HTTPS --> EXT
  REPO -- SQL --> DBX
```

## Key

| Notation | Meaning |
|---|---|
| «component» box | A replaceable part with a clear responsibility |
| Circle | An interface (a service offered or needed) |
| Line from a circle to a component | The component provides that interface |
| "requires" arrow | The component needs that interface |
| «external» | A system we do not build or control |

## Notes

- Expense Service depends on the `INotifier` interface, not on a specific provider. Changing the notification provider changes only the Notification Adapter.
- Budget Repository is the only component that runs SQL.
- Auth Guard checks the session before any expense logic runs.
