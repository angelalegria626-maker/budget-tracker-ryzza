# C4 Container Diagram for the Budget Tracker

```mermaid
flowchart TB
  S["<b>Student</b><br/>[Person]<br/>Boarding student with a weekly or monthly allowance"]
  subgraph SYS["Budget Tracker [Software System]"]
    W["<b>Web Application</b><br/>[Container: Next.js / React]<br/>Mobile-friendly pages for logging purchases, viewing balance, and history"]
    A["<b>API Application</b><br/>[Container: Next.js Route Handlers]<br/>Login, expense logging, balance and pace calculation, alert rules as JSON over HTTPS"]
    D[("<b>Database</b><br/>[Container: PostgreSQL]<br/>Users, allowance periods, expenses, alerts")]
  end
  N["<b>Notification Service</b><br/>[Software System, external]<br/>Delivers email or push alerts"]
  S -- "Uses [HTTPS]" --> W
  W -- "Makes API calls [JSON/HTTPS]" --> A
  A -- "Reads and writes [SQL/TLS]" --> D
  A -- "Requests alert delivery [HTTPS]" --> N
  N -. "Sends pace alerts to the student" .-> S
  style N stroke-dasharray: 6 4
```

## Key

| Notation | Meaning |
|---|---|
| Solid-bordered box | Element inside the scope being described |
| Dashed-bordered box | External software system we do not build or control |
| Large labelled frame | Boundary of the software system being zoomed into |
| Cylinder | Container that stores data |
| Solid arrow | Request or call, labelled with intent [technology] |
| Dashed arrow | Asynchronous message (an alert delivered later) |

## Containers

| Container | Technology | Responsibility |
|---|---|---|
| Web Application | Next.js / React | Pages for logging purchases, viewing balance and history |
| API Application | Next.js Route Handlers | Authentication, expense logging, balance and pace calculation, alert rules |
| Database | PostgreSQL | Stores users, allowance periods, expenses, alerts |

## Design note

We drew the Next.js app as **two containers** (web and API) because they have different responsibilities and callers.
