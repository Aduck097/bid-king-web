## Why

BidKing already has enough gameplay design material to support a playable browser prototype, but the repository does not yet contain the product docs, item data, or any implementation. We need a spec-driven first version that can run fully in the browser so the auction loop can be validated before adding backend persistence and multiplayer services.

## What Changes

- Add the current gameplay design documents and structured item seed data into the repository.
- Introduce a static web prototype that covers lobby navigation, map entry checks, role and tool loadout, five-round auction flow, settlement, shop purchases, and warehouse selling.
- Implement local browser persistence for money, warehouse, and tool inventory to support repeatable prototype testing without a backend.
- Add AI-driven opponents that can bid and use reveal tools inside the same local simulation.
- Add OpenSpec requirements for auction sessions, reveal tools, and inventory/shop behavior.

## Capabilities

### New Capabilities
- `auction-session`: Browser-based auction sessions with map gating, role loadout, round progression, bidding thresholds, AI opponents, and settlement.
- `reveal-tools`: Consumable reveal tools that players can buy, carry into matches, and use for private information gains with public usage logs.
- `inventory-and-shop`: Local warehouse and shop flows for selling collectibles and buying tool inventory in the browser prototype.

### Modified Capabilities
- None.

## Impact

- Adds product documentation and item seed data to the repository.
- Adds a static front-end implementation using HTML, CSS, and JavaScript.
- Introduces browser-side persistence with `localStorage`.
- Establishes the initial OpenSpec contract for future backend and persistence work.
