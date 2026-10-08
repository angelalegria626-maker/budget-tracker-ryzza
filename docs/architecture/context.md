# C4 System Context Diagram for the Budget Tracker

```mermaid
flowchart TB
  S["<b>Student</b><br/>[Person]<br/>Boarding student with a weekly or monthly allowance"]
  BT["<b>Budget Tracker</b><br/>[Software System]<br/>Lets students log small purchases in seconds, see their remaining allowance, and get pace alerts"]
  N["<b>Notification Service</b><br/>[Software System, external]<br/>Delivers email or push alerts"]
  S -- "Logs purchases, sets allowance, and checks balance" --> BT
  BT -- "Requests delivery of pace alerts" --> N
  N -. "Sends pace alerts to the student" .-> S
  style BT stroke-width:3px
  style N stroke-dasharray: 6 4
```

## Key

| Notation | Meaning |
|---|---|
| Thick-bordered box | The software system in focus |
| Dashed-bordered box | External software system we do not build or control |
| Solid arrow | Request or call, labelled with intent |
| Dashed arrow | Asynchronous message (an alert delivered later) |

## Narrative

The Student is the only user role. The Student logs purchases, sets an allowance, and checks the remaining balance in the Budget Tracker. When spending runs ahead of pace, the Budget Tracker asks an external Notification Service to deliver an alert. The system has no bank or e-wallet integration by design.
