# DROP SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Drop System.

The Drop System is responsible for managing all collectible drops
and distributing their effects to the appropriate systems.

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing drop or reward logic

---

## SYSTEM ROLE

The Drop System manages:

- spawning collectible drops
- updating drop movement and lifetime
- detecting player collection events
- routing rewards to the correct progression layer

The Drop System does NOT:

- decide when drops should occur
- apply combat logic
- manage player movement
- resolve collisions

---

## OWNERSHIP

The Drop System OWNS:

- drop entity data
- drop lifecycle (spawn → active → collected / expired)
- drop categorization and routing

The Drop System DOES NOT OWN:

- reward eligibility decisions
- meta-progression persistence
- run termination logic

---

## DROP CATEGORIES

Two distinct drop categories exist and MUST remain separated.

### 1. Coins (Meta Progression)

- Used for between-run progression
- Persist across runs
- Do not affect current combat state

### 2. Power-Ups (Run Progression)

- Affect player state during the current run
- Reset completely on death
- Are capped and explicitly limited

Mixing these categories is forbidden.

---

## DROP DEFINITION (DATA-DRIVEN)

Each drop instance is defined by data.

Mandatory fields:

- dropType (coin | powerUp)
- subtype (e.g. weapon, shield, hp)
- position
- lifetime
- value or effect descriptor

Optional fields:

- visualVariant
- attractionBehavior

---

## DROP SPAWNING

The Drop System spawns drops only upon explicit requests.

Valid request sources:

- Enemy System (on destruction)
- Boss System (on phase or defeat)
- Wave System (reward signals)

The Drop System MUST NOT:

- decide drop timing
- decide drop rarity

---

## COLLECTION MODEL

- Drops are collected when the player hitbox intersects the drop hitbox
- Collection is immediate and deterministic

Upon collection:

- coins are routed to meta-progression
- power-ups are routed to the Player System

---

## DROP MOVEMENT

- Drops may drift slowly
- Drops may optionally attract toward the player
- Attraction behavior MUST be simple and capped

Drops MUST NOT:

- chase the player aggressively
- affect player movement

---

## LIFETIME MANAGEMENT

A drop is removed when:

- collected by the player
- lifetime expires
- it exits the gameplay viewport

Removal MUST be immediate.

---

## PERFORMANCE CONSTRAINTS

- Drop count is limited and predictable
- Object pooling is mandatory
- No allocations during update

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- random reward mutation
- hidden stat changes
- power-ups affecting meta progression
- meta rewards affecting current run state

---

## INTEGRATION NOTES

- Collision System detects drop collection
- Player System applies run-based power-ups
- Meta progression system consumes coins
- Effect System handles visual feedback

The Drop System acts as a routing layer.

---

## FINAL RULE

If a drop implementation:

- mixes progression layers
- applies gameplay logic
- introduces randomness beyond configuration

It is incorrect and must be rejected.
