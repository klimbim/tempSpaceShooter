# PLAYER SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Player System.

The Player System is responsible for managing the player ship as a deterministic,
input-driven entity with clear feedback and strict separation of concerns.

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing player-related logic

---

## SYSTEM ROLE

The Player System manages:

- player state
- player movement
- player weapon firing
- player damage intake
- application of run-based upgrades

The Player System does NOT:

- resolve collisions
- manage projectiles
- manage drops or meta progression
- control camera or UI

---

## OWNERSHIP

The Player System OWNS:

- player entity data
- player movement state
- weapon configuration (current run)
- shield and HP values
- active run-based upgrades

The Player System DOES NOT OWN:

- input device handling (Input System)
- projectile lifecycle (Projectile System)
- collision detection (Collision System)
- visual effects (Effect System)

---

## PLAYER DEFINITION (DATA-DRIVEN)

The player ship is defined as a data entity.

Mandatory fields:

- position
- velocity
- maxSpeed
- acceleration
- hp
- shield
- hitbox
- weaponState

Optional fields:

- visualTiltState
- invulnerabilityTimer

The player MUST NOT contain autonomous logic.

---

## INPUT INTEGRATION

The Player System consumes abstract intent data:

- targetPosition
- fireActive
- specialActive
- pauseRequested

The Player System MUST NOT:

- read raw input events
- branch logic based on input device type

---

## MOVEMENT MODEL

- Movement is target-based
- Player accelerates toward targetPosition
- Maximum speed is capped
- Movement is deterministic

Rules:

- No inertia after input release
- Minor smoothing allowed
- Visual tilt does not affect logic

---

## WEAPON MODEL

- Player weapons fire automatically while fireActive is true
- Weapon behavior is determined by weaponState

Weapon upgrades may affect:

- number of firing lanes
- firing spread
- projectile type

Weapon upgrades:

- are capped (explicit max levels)
- apply only for the current run

---

## DAMAGE AND SHIELD MODEL

- Damage is received via Collision System events
- Shield absorbs damage first
- HP is reduced only when shield is depleted

Optional rules:

- short invulnerability window after hit

The Player System MUST NOT resolve collision detection.

---

## RUN-BASED UPGRADES

Run-based upgrades:

- are applied explicitly
- modify player state or weaponState
- reset completely on death

Meta progression is out of scope for this system.

---

## DEATH HANDLING

- Player death occurs when HP reaches zero
- Death triggers:

  - effect signals
  - run termination

The Player System does NOT restart the game.

---

## PERFORMANCE CONSTRAINTS

- Player update must be lightweight
- No allocations during update
- No dynamic creation of weapon logic

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- autonomous movement decisions
- player AI assistance
- adaptive difficulty logic
- hidden state transitions

---

## INTEGRATION NOTES

- Input System provides intent data
- Projectile System handles spawned bullets
- Collision System reports hit events
- Effect System handles visual feedback
- UI System reads player state

The Player System remains deterministic and input-driven.

---

## FINAL RULE

If a player implementation:

- embeds logic from other systems
- reacts unpredictably to input
- hides state changes

It is incorrect and must be rejected.
