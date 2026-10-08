# UML Package Diagram for the Budget Tracker Project

```mermaid
flowchart TB
  subgraph APP["«package» app (routes)"]
    P1["«package» (student) pages"]
    P2["«package» api route handlers"]
  end
  P3["«package» components"]
  subgraph LIB["«package» lib"]
    P4["«package» api-client"]
    P5["«package» domain"]
    P6["«package» db"]
    P7["«package» notifications"]
  end
  P1 -. "«import»" .-> P3
  P1 -. "«import»" .-> P4
  P4 -. "calls over HTTP [JSON]" .-> P2
  P2 -. "«import»" .-> P5
  P5 -. "«import»" .-> P6
  P5 -. "«import»" .-> P7
```

## Key

| Notation | Meaning |
|---|---|
| «package» box | A folder or module |
| Frame around boxes | A parent package containing sub-packages |
| Dashed arrow «import» | The source package uses the target package |

## Layering rule

Pages never import `lib/db` or `lib/notifications`; only `lib/domain` does, and pages reach the server only through `lib/api-client` and the API route handlers.

## Notes

- This matches the container diagram: the web pages call the API over HTTP and do not touch the database.
- Components map to folders: Expense Service, Pace Calculator and Auth Guard live in `lib/domain`; Budget Repository in `lib/db`; Notification Adapter in `lib/notifications`.
