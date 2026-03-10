## Context

The repository is currently empty aside from the license, while the local workspace already contains gameplay design markdown and a structured 504-item seed dataset. The first deliverable is not a production multiplayer system; it is a browser-only prototype that validates the player journey from map selection to settlement and warehouse/shop follow-up.

## Goals / Non-Goals

**Goals:**
- Preserve the current gameplay design as repository documentation.
- Build a single-browser playable prototype with the full auction loop.
- Persist enough local state to support repeated testing across page refreshes.
- Keep the implementation simple enough to evolve into a future service-backed version.

**Non-Goals:**
- Real account authentication.
- Real-time multiplayer networking.
- Backend APIs or MySQL integration.
- Final balancing for AI, economy, or tool prices.

## Decisions

### Use a static single-page browser app
A plain HTML/CSS/JavaScript application is the fastest way to validate the gameplay loop in this repository, which currently has no framework, build system, or deployment conventions. A framework would add setup cost without helping the first prototype requirements.

Alternative considered:
- Introduce a React/Vite stack immediately. Rejected for the prototype because the repository is empty and the first priority is validating gameplay rather than establishing a full front-end toolchain.

### Persist prototype progression with localStorage
Money, tool inventory, warehouse items, and session progress SHALL be stored in `localStorage` so the prototype survives refreshes and can mimic account progression without a backend.

Alternative considered:
- In-memory state only. Rejected because shop and warehouse flows lose value if the player state resets every refresh.

### Represent auction knowledge as separate public and private reveal records
The UI needs to show public logs, private role/tool information, and merged blind-box visual states. Maintaining explicit public/private reveal collections keeps rendering rules deterministic and avoids conflating visibility scopes.

Alternative considered:
- Render directly from ad hoc logs. Rejected because the blind-box view needs entity-level merge rules for quality-only, outline-only, and fully revealed items.

### Seed the prototype with the existing 504-item JSON data
The local dataset already contains category, quality, size, and fixed recycle price. Reusing it avoids redundant mock generation and makes settlement and warehouse selling meaningful.

Alternative considered:
- Generate smaller random placeholder items. Rejected because the data already exists and using it makes the prototype closer to the intended game.

## Risks / Trade-offs

- [Static app complexity] -> Keep the UI modular by page sections and separate state helpers inside `app.js`.
- [AI quality may feel weak] -> Start with deterministic heuristics based on known info, thresholds, and remaining budget rather than pretending to be fully adaptive.
- [Large single-file JavaScript] -> Acceptable for the first prototype, but code should be grouped by state, generators, auction flow, and rendering to keep later refactoring straightforward.
- [Economic balance is provisional] -> Treat prices and AI aggressiveness as prototype defaults, not final live values.

## Migration Plan

1. Add docs and seed data into the repository.
2. Add the browser prototype files and wire them to the local dataset.
3. Verify the prototype can complete full auction loops locally.
4. Push the spec and prototype as the first repository baseline.

## Open Questions

- Final money sinks and failure costs are still intentionally deferred.
- Tool assortment may be reduced or expanded after first playtests.
- Later backend integration will need a persistent user and match schema, but that is outside this change.
