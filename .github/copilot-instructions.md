# Copilot Instructions for C4-Modeling-in-Mermaid

This repository is a **documentation-only** collection of cheatsheets. There is no application code, build, or test suite — every change is a Markdown edit.

## What this repo is

- Cheatsheets for drawing C4 model diagrams (Context, Container, Component, Relationships/Layouts) using plain Mermaid `flowchart` syntax instead of Mermaid's native (but limited) `C4Context`/`C4Container`/`C4Component` diagram types.
- Each element maps back to its equivalent C4-PlantUML macro (e.g. `Person(...)`, `Container(...)`, `Rel(...)`) so PlantUML users can find the matching style.
- Files live in [C4-cheatsheets/](../C4-cheatsheets/), indexed from the root [README.md](../README.md).

## Conventions to follow when editing cheatsheets

Each cheatsheet file follows this structure — keep new content consistent with it:

1. **Color Palette** table (C4 blue theme: internal = blue `#1168bd`/dark blue `#08427b`, external = gray `#999999`).
2. **C4 PlantUML → Mermaid Flowchart Mapping** table.
3. **Element Index & Legend** — one consolidated `mermaid flowchart` block defining every `classDef` for that level plus example nodes, split into `internal`/`external` subgraphs.
4. **Complete Diagram Examples** — self-contained, copy-pasteable `mermaid` code blocks ranging from small to large/multi-subgraph.
5. **Best Practices** — do's and don'ts for that diagram level.
6. **Copy-Paste Template** — a blank skeleton to start a new diagram.

Rules:
- Every Mermaid snippet must be **self-contained** (includes its own `classDef` lines) so it renders correctly when copied in isolation.
- Use `classDef`/`class` for styling and `subgraph` for boundaries — do not use Mermaid's native `C4Context`/`C4Container`/`C4Component`/`C4Dynamic` syntax (see the "Why not mermaid's native C4 diagrams?" section in the README for rationale).
- Reuse the existing color hex values exactly; internal elements use the blue palette, external elements use gray.
- Keep table formatting aligned (Prettier with `proseWrap: preserve` formats Markdown on save — see [.prettierrc](../.prettierrc)).
- When adding a new element or diagram type, update all three tables (Color Palette, PlantUML Mapping, Element Index & Legend) and the root README index table if a new file is added.

## Validating changes

There is no build step. To validate a change, mentally (or visually, e.g. via the Mermaid Live Editor or the VS Code Markdown preview) confirm the `mermaid` code block is syntactically valid and renders as described.

## Consumer-Facing AI Components

This repo also ships GitHub Copilot customizations that let other projects generate C4 diagrams using these conventions (see the README's "Use These Cheatsheets with GitHub Copilot" section for install instructions aimed at consumers):

- [.github/skills/c4-mermaid-diagrams/](./skills/c4-mermaid-diagrams/) — the primary skill; bundles its own copies of the 4 cheatsheets under `references/` so it is self-contained and copy-paste-able into another project's `.github/skills/`.
- [.github/prompts/](./prompts/) — `c4-context`, `c4-container`, `c4-component`, `c4-relationships` slash commands for quick single-diagram generation.
- [.github/agents/c4-architect.agent.md](./agents/c4-architect.agent.md) — a custom agent that interviews the user and produces a linked Context/Container/Component diagram set.

**Maintenance rule:** `C4-cheatsheets/` is the canonical source. Whenever you edit a cheatsheet there, mirror the same change into the matching file under `.github/skills/c4-mermaid-diagrams/references/` and update its "Synced from ... on `<date>`" marker comment, so the bundled skill copy never drifts from the original.
