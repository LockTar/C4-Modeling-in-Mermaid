---
name: c4-mermaid-diagrams
description: 'Generate C4 model architecture diagrams (Context, Container, Component levels, plus Relationships/Layouts) as self-contained Mermaid flowcharts, following the C4-Modeling-in-Mermaid repo conventions. USE FOR: "create a C4 diagram", "architecture diagram", "system context diagram", "container diagram", "component diagram", "software architecture diagram in mermaid", "C4 model diagram", "draw system architecture", "visualize software architecture", "diagram my system/containers/components". DO NOT USE FOR: Mermaid native C4Context/C4Container/C4Component/C4Dynamic diagram syntax (deliberately avoided here in favor of plain flowchart + classDef/subgraph for full styling control).'
---

# C4 Mermaid Diagrams

Generate [C4 model](https://c4model.com/) architecture diagrams using plain Mermaid `flowchart` syntax + `classDef`/`class`/`subgraph` — never Mermaid's native `C4Context`/`C4Container`/`C4Component`/`C4Dynamic` types (styling, boundaries, and directional hints are unreliable there).

This skill is self-contained: everything needed is bundled in `references/`. It does not depend on any other folder in the consuming repo.

## Decision Flow

| User is asking about...                                    | Read this reference file                                              |
| ------------------------------------------------------------ | ----------------------------------------------------------------------- |
| People, systems, external systems, enterprise boundary       | `references/C4-Context-Diagram-Mermaid-Flowchart-Cheatsheet.md`         |
| Deployable units (apps, APIs, databases, queues)              | `references/C4-Container-Diagram-Mermaid-Flowchart-Cheatsheet.md`       |
| Internal structure of one container (controllers, services)   | `references/C4-Component-Diagram-Mermaid-Flowchart-Cheatsheet.md`       |
| Arrow direction, `Rel`/`BiRel`, layout-only positioning        | `references/C4-Relationships-Layouts-Cheatsheet.md`                     |
| "Show me this system end-to-end" / multiple levels            | Read Context first, then Container, then Component — reuse names/colors across all three |

## Core Conventions (apply to every diagram you generate)

- Every snippet is **self-contained**: include all `classDef` lines it uses, even if you already defined them earlier in the conversation.
- Style with `classDef` + `class`, and group with `subgraph` — never use `C4Context`/`C4Container`/`C4Component`/`C4Dynamic`.
- Reuse the exact palette hex values — do not invent new colors:
  - Internal: medium blue `#1168bd` (fill), dark blue `#08427b` (Person fill), stroke `#073b6f`/`#0f5daf`.
  - External: gray `#999999` (fill), stroke `#8a8a8a`.
  - Boundaries: `fill:none,stroke:#999,stroke-width:2px,stroke-dasharray: 5 5,color:#444` (dashed).
- Label every element with its C4 type in brackets, e.g. `[Person]`, `[Software System]`, `[Container]`, `[Component]`, `[Database]`, `[External System]`.
- Keep each diagram to one C4 level (Context OR Container OR Component) — do not mix levels of detail in a single diagram.
- Include the technology/protocol in relationship labels where relevant (e.g. `-->|"REST/JSON"|`).

## Workflow

1. Identify which C4 level(s) the user needs (see Decision Flow above). If ambiguous, ask.
2. Read the full matching reference file(s) before drafting — they contain the exact `classDef` lines, node/shape syntax, and worked examples to copy from.
3. Draft the diagram, reusing the reference file's shapes (rounded rect for `Person`, cylinder for `*Db`, dashed shape for `*Queue`, dashed subgraph for boundaries) and exact hex values.
4. Validate against the checklist below before returning the result.
5. Return one self-contained ```mermaid``` code block. Briefly note which cheatsheet/level it corresponds to.

## Validation Checklist

- [ ] Snippet is self-contained (all `classDef` used are defined in this same block).
- [ ] No native `C4Context`/`C4Container`/`C4Component`/`C4Dynamic` syntax used.
- [ ] Colors match the palette exactly (internal blue, external gray, dashed gray boundaries).
- [ ] Every element has a bracketed C4 type label.
- [ ] Single C4 level per diagram; boundaries use `subgraph` + the matching `*Boundary` classDef.
- [ ] Relationships are labeled with interaction + protocol/technology where known.

## Bundled References

- `references/C4-Context-Diagram-Mermaid-Flowchart-Cheatsheet.md`
- `references/C4-Container-Diagram-Mermaid-Flowchart-Cheatsheet.md`
- `references/C4-Component-Diagram-Mermaid-Flowchart-Cheatsheet.md`
- `references/C4-Relationships-Layouts-Cheatsheet.md`

These are copies mirrored from this repo's `C4-cheatsheets/` folder (see the sync marker at the top of each file). If you are working inside the `C4-Modeling-in-Mermaid` repo itself, treat `C4-cheatsheets/` as canonical and keep these copies in sync when it changes.
