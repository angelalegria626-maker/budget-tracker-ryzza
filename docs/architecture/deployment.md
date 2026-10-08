# UML Deployment Diagram for the Budget Tracker (Provisional)

```mermaid
flowchart LR
  subgraph PH["«device» Student's smartphone"]
    subgraph BR["«execution environment» Mobile browser"]
      A1["«artifact» Web UI bundle (HTML/JS)"]
    end
  end
  subgraph HOST["«node» Cloud hosting platform (provider to be chosen)"]
    subgraph RT["«execution environment» Node.js runtime"]
      A2["«artifact» Next.js app (pages + API routes)"]
    end
  end
  subgraph DBN["«node» Managed database service (provider to be chosen)"]
    A3[("«artifact» PostgreSQL database")]
  end
  NS["«external system»<br/>Notification Service"]
  BR -- "HTTPS" --> RT
  RT -- "TLS / SQL" --> DBN
  RT -- "HTTPS (API key in env var)" --> NS
  NS -. "email or push delivery" .-> PH
```

## Key

| Notation | Meaning |
|---|---|
| «device» / «node» | A machine or service where software runs |
| «execution environment» | Software that runs artifacts (browser, runtime) |
| «artifact» | A deployable file or unit |
| Solid line | Communication path, labelled with its protocol |
| Dashed line | Asynchronous delivery |

## Notes

- Provisional: provider names are generic and will be finalized in Week 12.
- Web Application and API Application from the container diagram ship together as one Next.js artifact. The Database runs on the managed database node.
- The notification provider's API key lives in an environment variable on the server, never in the browser bundle.
- No secrets or real addresses appear in this diagram.
