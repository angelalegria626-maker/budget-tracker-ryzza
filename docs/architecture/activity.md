# UML Activity Diagram for the Budget Tracker: Logging a Purchase

```mermaid
flowchart TD
  subgraph ST["Student"]
    A0(( )) --> A1[Buy something]
    A2[Enter amount and note]
    A3[Fix the entry]
    A4[Set allowance and period]
    A9[See updated balance and alert]
    A10(((" ")))
  end
  subgraph SY["System"]
    B1{Active allowance period?}
    B2{Entry valid?}
    B3[Save purchase]
    B4[Recalculate remaining balance]
    B5{Spending ahead of pace?}
    B6[Request pace alert]
    B7[Show updated balance]
  end
  A1 --> A2 --> B1
  B1 -- "[no]" --> A4 --> A2
  B1 -- "[yes]" --> B2
  B2 -- "[no]" --> A3 --> A2
  B2 -- "[yes]" --> B3 --> B4 --> B5
  B5 -- "[yes]" --> B6 --> B7
  B5 -- "[no]" --> B7
  B7 --> A9 --> A10
```

## Key

| Notation | Meaning |
|---|---|
| Small circle | Start of the activity |
| Double circle | End of the activity |
| Rectangle | An action, named with a verb |
| Diamond | A decision; every outgoing arrow has a guard in [brackets] |
| Large frame (lane) | Who is responsible for the actions inside it |

## Notes

- Mermaid has no dedicated activity diagram type, so this flowchart approximates UML notation.
- This is the core workflow because logging purchases is what the Budget Tracker exists to support.
- The pace alert itself is delivered later by the external Notification Service, shown as an asynchronous message in the sequence diagram.
- Use cases realized here: Set allowance and period, Log purchase, View remaining balance, Receive pace alert.
