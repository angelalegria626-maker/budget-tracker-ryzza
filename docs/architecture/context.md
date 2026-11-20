# C4 System Context Diagram for the Budget Tracker

```mermaid
flowchart TB
  Student["<b>Student</b><br/>[Person]<br/>A college student boarding away from home who receives a weekly allowance"]
  System["<b>Budget Tracker</b><br/>[Software System]<br/>Lets a student log small purchases in seconds, see the remaining allowance and how long it will last, and track a savings goal"]

  Student -->|"Sets allowance, logs purchases, sets savings goals"| System
  System -->|"Shows balance, runway, categories, savings progress and pace alerts"| Student

  classDef person fill:#dbeafe,stroke:#2563eb,color:#000
  classDef system fill:#ede9fe,stroke:#7c3aed,color:#000
  class Student person
  class System system
```

## Notes

- **Audience / risk:** instructors and stakeholders; it shows the system boundary at a glance.
- No external systems appear. The MVP has no bank, payment or notification integrations.
