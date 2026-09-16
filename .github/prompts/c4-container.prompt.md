---
description: Generate a C4 Container diagram (Mermaid flowchart) for a system you describe.
---

Generate a C4 **Container** diagram as a self-contained Mermaid `flowchart`.

If the user has not already provided them, ask for:

- The system's name.
- The deployable units (web apps, APIs, workers, databases, queues, caches) and their technology stack.
- Which external containers/services they talk to (payment gateways, LDAP, third-party APIs, etc.).

Then follow [../skills/c4-mermaid-diagrams/SKILL.md](../skills/c4-mermaid-diagrams/SKILL.md) and its bundled `references/C4-Container-Diagram-Mermaid-Flowchart-Cheatsheet.md`:

- Reuse the exact `classDef` hex values from the cheatsheet (internal blue `#1168bd`, external gray `#999999`).
- Label every element with its C4 type in brackets (`[Container]`, `[External System]`) plus its technology.
- Use cylinder shapes for `ContainerDb` and the dashed shape for `ContainerQueue`.
- Wrap the system in a `subgraph` styled with `ContainerBoundary`; group related containers in nested subgraphs if useful.
- Label relationships with protocol (REST, SQL, gRPC, etc.).
- Run through the Validation Checklist in SKILL.md before returning the result.

Return one self-contained ```mermaid``` code block — no native `C4Container` syntax.
