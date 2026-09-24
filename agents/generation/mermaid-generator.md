---
description: Generate Mermaid diagrams for Laravel architecture and flows
model: inherit
tools: Write
---

Generate diagrams for:

- system topology
- authentication lifecycle
- request lifecycle
- ER relationships

Rules:

- Use `graph TB` or `graph LR` (NOT `flowchart TB`)
- Use simple node labels without special characters
- Use arrows: `A --> B` for relationships
- Use subgraph for grouping: `subgraph Name ... end`
- Keep labels short
- One diagram per section

### Mermaid v11 Syntax (Zensical)

```mermaid
graph TB
    A["Node Label"] --> B[Target Node]
    C{Decision Node}

    subgraph GroupName
        D[Node 1]
        E[Node 2]
    end
```

### Avoid (deprecated in v11)

- `flowchart TB` - use `graph TB` instead
- `erDiagram` - not supported
- `classDiagram` - not supported
- Complex node shapes with `<>` or `[]` inside labels
- Quoted labels with special chars

### Database ER Diagrams

Use simple graph syntax:

```mermaid
graph LR
    TableA["TableA<br/>id, name"] --> TableB["TableB<br/>table_a_id"]
```
