---
description: Adjust arrow directions, relationship labels, or layout of an existing C4 Mermaid flowchart.
---

Adjust the relationships and/or layout of a C4 Mermaid `flowchart` diagram.

If the user has not already provided it, ask for the existing Mermaid diagram (or the elements/relationships they want) and what they want changed (direction, bidirectionality, grouping).

Then follow [../skills/c4-mermaid-diagrams/SKILL.md](../skills/c4-mermaid-diagrams/SKILL.md) and its bundled `references/C4-Relationships-Layouts-Cheatsheet.md`:

- Mermaid has no per-edge direction override like C4-PlantUML's `Rel_U/D/L/R` — direction is controlled by the flowchart's declared direction (`TB`, `BT`, `LR`, `RL`). Pick the orientation matching the dominant flow.
- Use `-->` for one-directional relationships and `<-->` for true mutual/peer interactions (`BiRel`).
- Label every relationship with the interaction and protocol/technology.
- Keep the diagram self-contained (include all `classDef` lines it uses).

Return one self-contained ```mermaid``` code block.
