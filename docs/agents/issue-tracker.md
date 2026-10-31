# Issue tracker

Specs and issues live as Markdown files under `.scratch/`.

## Conventions

- One feature or effort per directory: `.scratch/<feature-slug>/`.
- Specifications: `.scratch/<feature-slug>/spec.md`.
- Implementation tickets: one file per ticket under
  `.scratch/<feature-slug>/issues/<NN>-<slug>.md`.
- Number implementation tickets from `01` in dependency order.
- Record ticket status near the top using the vocabulary in
  `triage-labels.md`.
- Record dependencies in a `Blocked by:` field using ticket
  numbers and titles.
- Append discussion under `## Comments`.

## Publishing and fetching

When a skill says to publish, create the relevant local file.
When it says to fetch a ticket, read the referenced file.
Publish implementation tickets individually.

## Wayfinding operations

- Map: `.scratch/<effort>/map.md`.
- Decision tickets: `.scratch/<effort>/issues/NN-<slug>.md`.
- Record ticket type as `Type: research`, `prototype`,
  `grilling`, or `task`.
- Record dependencies in `Blocked by: NN, NN`.
- Claim a ticket by saving `Status: claimed` before working.
- Resolve it by appending `## Answer` and saving
  `Status: resolved`.
- Add a short answer summary and ticket link to the map's
  Decisions so far section.
- The frontier consists of open, unclaimed tickets whose
  blockers are all resolved, ordered by ticket number.

Decision-ticket lifecycle states are separate from triage labels.
