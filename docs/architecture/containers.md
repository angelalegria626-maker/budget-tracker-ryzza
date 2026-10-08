# C4 Container Diagram for the Budget Tracker

```mermaid
flowchart TB
  S["<b>Student</b><br/>[Person]<br/>Boarding student on a weekly or monthly allowance"]
  subgraph BT["Budget Tracker [Software System]"]
    W["<b>Web Application</b><br/>[Container: Next.js, React]<br/>Mobile-friendly pages for setting an allowance, logging purchases and viewing the balance"]
    A["<b>API Application</b><br/>[Container: Next.js route handlers, Node.js]<br/>Validates requests, calculates remaining balance and pace, creates pace alerts"]
    D[("<b>Database</b><br/>[Container: relational database]<br/>Stores students, allowance periods, expenses and pace alerts")]
  end
  S -->|"Logs purchases and views the balance [HTTPS]"| W
  W -->|"Sends requests for periods, expenses and balance [JSON over HTTPS]"| A
  A -->|"Reads and writes student data [SQL over TLS]"| D
```

**Next.js decision:** we drew the Next.js app as two containers, a Web Application (pages that run in the student's browser) and an API Application (route handlers on the server), even though both are built and deployed together as one Next.js project.

## Key

| Notation | Meaning |
|---|---|
| Rectangle [Container] | A separately running unit, with its technology |
| Cylinder | A database container |
| Frame | The system boundary |
| Arrow with label | Intent of the call, and the protocol in square brackets |

## Notes

- **Audience / risk:** developers and the instructor; it reduces the risk of unclear technology and responsibility boundaries.
- The Web Application never talks to the Database directly.
- The database provider is not chosen yet (see `deployment.md`).
