## ADDED Requirements

### Requirement: Reveal tools SHALL be consumable, public-to-use, and private-in-result
The system SHALL let players buy tool inventory outside matches, carry at most one copy of each chosen tool type into a match, consume at most one tool per round, show tool usage publicly, and keep the revealed results private to the tool owner.

#### Scenario: Player carries unique tools into a match
- **WHEN** the player confirms a loadout for an auction session
- **THEN** the system MUST allow at most five tool types and MUST reject duplicate copies of the same tool in the same match

#### Scenario: Tool usage is visible but result is private
- **WHEN** a participant uses a tool during a round
- **THEN** the public log MUST show which tool was used and the reveal result MUST only be visible in that participant's private information area

#### Scenario: Tool is consumed after use
- **WHEN** a participant uses a tool in a round
- **THEN** the system MUST mark that tool as spent for the current match and MUST NOT allow it to be used again in later rounds of the same match

### Requirement: Tool reveals SHALL update blind-box visualization consistently
The system SHALL merge tool and role reveal data into a single blind-box knowledge model that can display quality-only reveals, outline-only reveals, and full reveals without duplicating the same item.

#### Scenario: Quality-only reveal creates a color marker
- **WHEN** a reveal identifies only an item's quality
- **THEN** the system MUST display a single colored cell marker for that known item state

#### Scenario: Outline-only reveal creates a white outline
- **WHEN** a reveal identifies only an item's outline
- **THEN** the system MUST display the item's outline in white without assigning a quality color

#### Scenario: Later reveals complete the same item
- **WHEN** a later reveal provides the missing quality or outline for a previously known item
- **THEN** the system MUST merge the data into one displayed item state instead of rendering a duplicate marker
