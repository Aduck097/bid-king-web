## ADDED Requirements

### Requirement: Browser auction sessions SHALL support the full five-round prototype loop
The system SHALL let a player start a browser-local auction session by selecting a map, passing the entry-funds check, choosing one role, choosing up to five different tools, matching with three AI opponents, and playing through up to five bidding rounds before settlement.

#### Scenario: Player starts an eligible auction session
- **WHEN** the player selects a map they can afford and confirms role and tool loadout
- **THEN** the system starts a new auction session with one random subscene, one generated blind box, and three AI opponents

#### Scenario: Player is blocked from an ineligible map
- **WHEN** the player selects a map whose entry funds exceed their current money
- **THEN** the system MUST prevent session start and show that the map is locked for insufficient funds

### Requirement: Auction rounds SHALL apply the configured threshold rules
The system SHALL resolve each round with one public information reveal, automatic role information, at most one tool use per participant, one bid submission per participant, and a round-ending purchase check using the round threshold.

#### Scenario: Early purchase threshold is not met
- **WHEN** a round ends before round five and the top bid is below the current threshold against the second-highest bid
- **THEN** the system MUST continue the session into the next round

#### Scenario: Threshold is met before round five
- **WHEN** a round ends before round five and the top bid is greater than or equal to the current threshold against the second-highest bid
- **THEN** the system MUST end the auction and advance to settlement with the top bidder as winner

#### Scenario: Round five resolves by highest bid
- **WHEN** round five ends
- **THEN** the system MUST award the blind box to the highest bidder without applying earlier threshold multipliers

### Requirement: Settlement SHALL reveal items and support immediate color-based selling
The system SHALL transition the winning session into settlement, reveal all item outlines first, reveal full item information using quality-based delays, track running profit and loss against the winning bid, and allow selling warehouse items by selected colors before finishing settlement.

#### Scenario: Settlement reveals full information progressively
- **WHEN** settlement starts
- **THEN** the system MUST show all item outlines immediately and reveal each item's final details using the configured delay for its quality tier

#### Scenario: Player sells selected colors during settlement
- **WHEN** the player confirms settlement with one or more colors selected for sale
- **THEN** the system MUST sell all won items matching those colors, credit the player money by their fixed recycle prices, and keep unselected colors in the warehouse
