# UML Use Case Diagram for the Budget Tracker MVP

```mermaid
flowchart LR
  S["«actor»<br/>Student"]
  subgraph SYS["Budget Tracker (system boundary)"]
    UC1([Register / Log in])
    UC2([Set allowance and period])
    UC3([Log purchase])
    UC4([View remaining balance])
    UC5([View spending history])
    UC6([Edit or delete purchase])
    UC7([Receive pace alert])
  end
  N["«actor»<br/>Notification Service"]
  S --- UC1
  S --- UC2
  S --- UC3
  S --- UC4
  S --- UC5
  S --- UC6
  S --- UC7
  UC7 -. "«extend»" .-> UC3
  UC7 --- N
```

## Key

| Notation | Meaning |
|---|---|
| «actor» box | A role or external system outside the Budget Tracker |
| Oval | A goal the actor achieves (verb + object) |
| Large frame | System boundary: what is inside the Budget Tracker |
| Solid line | The actor takes part in that use case |
| Dashed arrow «extend» | Optional behaviour added to the base use case under a condition |

## Notes

- Mermaid has no dedicated use case diagram type, so this flowchart approximates UML notation.
- "Receive pace alert" extends "Log purchase" because the alert happens only when spending is ahead of pace.
- Actors match the context diagram: Student and Notification Service.
- Not in this MVP: export history and upgrade to premium (paid tier).

## Use cases and MVP features

| Use case | MVP feature it comes from |
|---|---|
| Register / Log in | Accounts for students |
| Set allowance and period | Weekly or monthly allowance setup |
| Log purchase | Quick logging in under 5 seconds |
| View remaining balance | Real-time remaining balance |
| View spending history | Review past purchases |
| Edit or delete purchase | Correct logging mistakes |
| Receive pace alert | Gentle alert when spending is ahead of pace |
