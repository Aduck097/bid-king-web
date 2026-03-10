## ADDED Requirements

### Requirement: The browser prototype SHALL provide local warehouse and shop flows
The system SHALL provide a warehouse view for stored collectibles and a shop view for buying tool inventory, with both areas backed by local browser persistence.

#### Scenario: Player buys tools from the shop
- **WHEN** the player purchases a tool they can afford from the shop
- **THEN** the system MUST deduct the tool price from current money and increase the stored inventory count for that tool

#### Scenario: Player sells a warehouse collectible directly
- **WHEN** the player sells an item from the warehouse view
- **THEN** the system MUST remove that item from storage and credit the player's money by that item's fixed recycle price

### Requirement: Prototype progression SHALL persist across refreshes
The system SHALL persist money, owned tools, warehouse contents, and last-known prototype progress in local browser storage so the player can continue testing after reloading the page.

#### Scenario: State is restored after refresh
- **WHEN** the player refreshes the browser after buying tools or storing collectibles
- **THEN** the system MUST restore the saved money, tool inventory, and warehouse contents from local storage
