# BidKing Web

BidKing Web is a browser-first prototype for the blind-box auction game loop.

## Repository Contents

- `docs/`: gameplay design markdown for maps, roles, items, tools, auction flow, and todo tracking
- `data/`: structured seed data used by the prototype
- `openspec/`: change-driven specification artifacts

## Current Scope

This repository currently targets a local web prototype only:
- map selection with entry-funds gating
- role and tool loadout
- five-round blind-box auction flow
- AI opponents
- settlement, warehouse, and shop flows
- local browser persistence

Backend services, MySQL persistence, and multiplayer networking are intentionally deferred until the prototype gameplay is validated.
