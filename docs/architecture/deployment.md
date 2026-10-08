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
    A3[("«artifact» Relational database")]
  end
  BR -- "HTTPS" --> RT
  RT -- "TLS / SQL" --> DBN
```

## Key

| Notation | Meaning |
|---|---|
| «device» / «node» | A machine or service where software runs |
| «execution environment» | Software that runs artifacts (browser, runtime) |
| «artifact» | A deployable file or unit |
| Solid line | Communication path, labelled with its protocol |

## Notes

- **Audience / risk:** the team and whoever deploys; it reduces the risk of surprises in hosting and cost. Provisional: provider names are generic until chosen.
- The Web Application and API Application from `containers.md` ship together as one Next.js artifact. The Database runs on the managed database node.
- The student needs only a phone browser; no app install, no bank linking.
- No secrets or real addresses appear in this diagram.
