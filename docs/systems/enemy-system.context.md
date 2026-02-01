# ENEMY SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Enemy System.

The Enemy System is responsible for instantiating and updating enemy entities
according to wave instructions and predefined behavior patterns.

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing enemy logic

---

## SYSTEM ROLE

The Enemy System manages enemy entities as scripted actors.

It:

- spawns enemies on request from the Wave System
- updates enemy state deterministically
- applies movement and shooting patterns assigned at spawn
- exposes enemy hitboxes and state for other systems

The Enemy System does NOT:

- decide when enemies appear (Wave System)
- define movement logic (Movement Patterns)
- handle projectile logic (Projectile System)
- resolve collisions or damage (Collision System)

---

## OWNERSHIP

The Enemy System OWNS:

- enemy entity data
- enemy lifecycle (spawn → active → destroyed)
- assignment of movement and shooting patterns
- enemy visibility state (active / inactive)

The Enemy System DOES NOT OWN:

- wave sequencing
- collision detection
- damage calculation
- drop spawning

---

## ENEMY DEFINITION (DATA-DRIVEN)

Enemies are defined purely as data configurations.

Each enemy instance includes:

- enemyType
- position
- hp
- hitbox
- movementPattern
- shootPattern
- phase (optional)

Enemies MUST NOT contain autonomous decision logic.

---

## ENEMY LIFECYCLE

1. Spawned by Wave System request
2. Activated when entering viewport
3. Updated each frame while active
4. Receives hit events from Collision System
5. Marked destroyed when HP reaches zero
6. Removal signaled to Effect and Drop Systems

Lifecycle transitions MUST be explicit.

---

## VISIBILITY AND ACTIVITY

- Enemies are updated only while inside the gameplay viewport
- Off-screen enemies are inactive and do not update
- Enemies may enter and exit the viewport only via wave design

Enemy activation is NOT dynamic.

---

## MOVEMENT INTEGRATION

- Enemy movement is defined via Movement Patterns
- Movement patterns are assigned at spawn
- Patterns may change only via explicit phase transitions

The Enemy System does NOT compute movement paths.

---

## SHOOTING INTEGRATION

- Enemy shooting behavior is defined by shoot patterns
- Shoot patterns determine:

  - firing rate
  - projectile configuration
  - firing offsets

The Enemy System requests projectile spawns but does not manage projectiles.

---

## PHASE SUPPORT (OPTIONAL)

Enemies MAY support multiple phases.

A phase transition:

- is triggered by explicit conditions (e.g. HP threshold)
- switches movement and/or shooting patterns

Implicit or reactive phase changes are forbidden.

---

## DAMAGE HANDLING

- Damage is applied only via Collision System events
- Enemy System updates HP based on damage events
- Visual feedback is delegated to Effect System

Enemy System MUST NOT resolve collision logic.

---

## PERFORMANCE CONSTRAINTS

- Enemy count per wave is limited and predictable
- No per-enemy allocation during update
- No dynamic behavior generation

Enemy updates must remain lightweight.

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- autonomous AI decision-making
- enemies reacting to player skill or position
- enemy-to-enemy collision or interaction
- dynamic difficulty adjustments

---

## INTEGRATION NOTES

- Wave System controls spawn timing
- Movement Patterns control trajectories
- Projectile System handles all bullets
- Collision System reports hit events
- Drop System handles rewards

The Enemy System acts as a deterministic executor.

---

## FINAL RULE

If an enemy implementation:

- introduces decision-making
- queries player state
- embeds movement or shooting logic

It is incorrect and must be rejected.
