---
description: Generate a C4 Context diagram (Mermaid flowchart) for a system you describe.
---

Generate a C4 **Context** diagram as a self-contained Mermaid `flowchart`.

If the user has not already provided them, ask for:

- The system's name and a one-line purpose.
- Primary actors/personas (internal and external), e.g. Customer, Admin, Partner.
- External systems it integrates with (payment gateways, auth providers, mail services, etc.).

Then follow [../skills/c4-mermaid-diagrams/SKILL.md](../skills/c4-mermaid-diagrams/SKILL.md) and its bundled `references/C4-Context-Diagram-Mermaid-Flowchart-Cheatsheet.md`:

- Reuse the exact `classDef` hex values from the cheatsheet (internal blue `#1168bd`/`#08427b`, external gray `#999999`).
- Label every element with its C4 type in brackets (`[Person]`, `[Software System]`, `[External System]`).
- Wrap the system boundary in a `subgraph` styled with `SystemBoundary`.
- Label relationships with the interaction and protocol/technology.
- Run through the Validation Checklist in SKILL.md before returning the result.

Return one self-contained ```mermaid``` code block — no native `C4Context` syntax.
