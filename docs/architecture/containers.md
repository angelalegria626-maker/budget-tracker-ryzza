# C4 Container Diagram for the Budget Tracker

```mermaid
flowchart TB
  Student["<b>Student</b><br/>[Person]<br/>Boarding student on a weekly allowance"]

  subgraph System["Budget Tracker [Software System]"]
    Web["<b>Web Application</b><br/>[Container: Next.js, React]<br/>Mobile-friendly pages for setting an allowance, logging purchases, viewing balance and runway, and tracking savings goals"]
    Api["<b>API Application</b><br/>[Container: Next.js route handlers, Node.js]<br/>Validates requests, assigns categories, calculates balance, pace and runway, creates pace alerts, updates savings goals"]
    Db[("<b>Database</b><br/>[Container: relational database]<br/>Stores students, allowance periods, expenses, pace alerts and savings goals")]
  end

  Student -->|"Uses [HTTPS]"| Web
  Web -->|"Sends requests [JSON over HTTPS]"| Api
  Api -->|"Reads and writes data [SQL over TLS]"| Db

  classDef person fill:#dbeafe,stroke:#2563eb,color:#000
  classDef container fill:#ede9fe,stroke:#7c3aed,color:#000
  class Student person
  class Web,Api,Db container
```

## Notes

- **Audience / risk:** developers; it shows the three deployable parts and how they talk.
- Only the API Application talks to the database.
- Only the text of the descriptions changed. The three containers are the same.
