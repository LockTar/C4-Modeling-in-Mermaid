---
description: Generate a C4 Component diagram (Mermaid flowchart) for one container you describe.
---

Generate a C4 **Component** diagram as a self-contained Mermaid `flowchart`.

If the user has not already provided them, ask for:

- The single container this diagram is for (e.g. "the Order API"), and its technology.
- The components inside it (controllers, services, repositories, event handlers) and how they group by layer.
- The external things it talks to (databases, message queues, external APIs/libraries).

Then follow [../skills/c4-mermaid-diagrams/SKILL.md](../skills/c4-mermaid-diagrams/SKILL.md) and its bundled `references/C4-Component-Diagram-Mermaid-Flowchart-Cheatsheet.md`:

- Reuse the exact `classDef` hex values from the cheatsheet (internal blue `#1168bd`, external gray `#999999`).
- Label every element with `[Component]`, and use cylinder shapes for `ComponentDb` and the dashed shape for `ComponentQueue`.
- Group components by layer/feature using nested subgraphs (e.g. Controllers, Services, Repositories).
- Stay at a single container's internal structure — do not mix in Context or Container-level elements.
- Run through the Validation Checklist in SKILL.md before returning the result.

Return one self-contained ```mermaid``` code block — no native `C4Component` syntax.
