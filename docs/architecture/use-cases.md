# UML Use Case Diagram for the Budget Tracker

```mermaid
flowchart LR
  Student["Student<br/>«actor»"]

  subgraph System["Budget Tracker"]
    UC1(["Create account"])
    UC2(["Sign in"])
    UC3(["Set allowance period"])
    UC4(["View remaining balance"])
    UC5(["Log purchase"])
    UC6(["Receive pace alert"])
    UC7(["Auto-assign expense category"])
    UC8(["View allowance runway"])
    UC9(["Set savings goal"])
    UC10(["Add to savings"])
    UC11(["View savings progress"])
  end

  Student --- UC1
  Student --- UC2
  Student --- UC3
  Student --- UC4
  Student --- UC5
  Student --- UC8
  Student --- UC9
  Student --- UC10
  Student --- UC11
  Student --- UC6

  UC6 -.->|"«extend»"| UC5
  UC5 -.->|"«include»"| UC7

  classDef actor fill:#dbeafe,stroke:#2563eb,color:#000
  classDef uc fill:#ede9fe,stroke:#7c3aed,color:#000
  class Student actor
  class UC1,UC2,UC3,UC4,UC5,UC6,UC7,UC8,UC9,UC10,UC11 uc
```

## Key

| Notation | Meaning |
|---|---|
| Blue box | The actor (the Student) |
| Rounded shape | A use case inside the system boundary |
| Solid line | The actor takes part in the use case |
| Dotted arrow «extend» | An optional behaviour added to the base use case |
| Dotted arrow «include» | Behaviour that is always part of the base use case |

## Notes

- **Audience / risk:** everyone; it fixes the MVP scope so nobody builds features that were not agreed.
- Receive pace alert extends Log purchase: it only happens when a purchase puts spending ahead of pace.
- Log purchase always includes Auto-assign expense category, so the student never picks a category by hand.
- View allowance runway, Set savings goal, Add to savings and View savings progress are the three new features: Allowance Runway, Smart Expense Categories (via the include) and Savings Goal Tracker.
- There is no "view history" or "export" use case. Those are future work.
