# C4 System Context Diagram for the Budget Tracker

```mermaid
flowchart TB
  S["<b>Student</b><br/>[Person]<br/>A college student boarding away from home who receives a weekly or monthly allowance"]
  BT["<b>Budget Tracker</b><br/>[Software System]<br/>Lets a student log small purchases in seconds, see the remaining allowance, and get a gentle alert when spending is ahead of pace"]
  S -->|"Sets an allowance period, logs purchases and checks the remaining balance"| BT
  BT -->|"Shows the remaining balance and a pace alert"| S
```

## Key

| Notation | Meaning |
|---|---|
| Box marked [Person] | A user role |
| Box marked [Software System] | The system we are building, drawn as one box |
| Arrow with label | A relationship, labelled with what the sender is trying to do |

## Notes

- **Audience / risk:** shared by the team, the instructor and non-technical readers; it reduces the risk of building the wrong scope.
- The only user role is the Student. Boarding house owners and campus orgs on the Lean Canvas are marketing channels, not users of the system.
- There are no external systems in the MVP. The Lean Canvas excludes bank linking, and payments (the paid tier) are not part of the MVP.
- Source: Lean Canvas (Customer Segments, Solution) and Javelin board, Experiment 1.
