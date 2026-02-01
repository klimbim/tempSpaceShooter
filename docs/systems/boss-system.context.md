# BOSS SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Boss System.

The Boss System is responsible for managing boss entities as structured, multi-phase encounters.

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing boss logic

---

## SYSTEM ROLE

The Boss System manages bosses as scripted, deterministic encounters.

It:

- spawns and initializes bosses when requested
- manages boss phases and phase transitions
- assigns movement and shooting patterns per phase
- aggregates boss state for UI (e.g., boss health bar)

The Boss System does NOT:

- control wave sequencing outside boss encounters
- implement movement logic (Movement Patterns)
- manage projectiles (Projectile System)
- resolve collisions or damage (Collision System)

---

## OWNERSHIP

The Boss System OWNS:

- boss entity data
- boss phase definitions
- phase transition state
- optional boss modules and their state

The Boss System DOES NOT OWN:

- generic enemy spawning
- collision detection
- drop spawning
- visual effects

---

## BOSS DEFINITION (DATA-DRIVEN)

Bosses are defined purely by data configurations.

Each boss definition includes:

- bossId
- basePosition
- totalHP or moduleHP definitions
- phases (ordered list)
- optional modules (sub-entities)

Bosses MUST NOT contain autonomous decision logic.

---

## PHASE MODEL

A boss encounter is divided into explicit phases.

Each phase defines:

- movementPattern
- shootPatterns
- duration or endCondition
- visualState (optional)

Phase transitions:

- are explicit
- are deterministic
- occur only when conditions are met

Implicit or reactive phase changes are forbidden.

---

## PHASE TRANSITIONS

A phase transition may be triggered by:

- elapsed time
- HP threshold
- destruction of required modules

Transitions MUST:

- be declared in data
- occur once per condition

---

## MODULE SUPPORT (OPTIONAL)

Bosses MAY be composed of multiple modules.

Each module:

- has its own HP and hitbox
- may have independent shoot patterns
- reports destruction to the Boss System

Boss completion conditions:

- all required modules destroyed
- or core HP reaches zero

Module order dependencies MUST be explicit.

---

## MOVEMENT INTEGRATION

- Boss movement uses Movement Patterns
- Movement patterns may change per phase
- Bosses generally remain within the upper gameplay area

Bosses MUST NOT chase the player.

---

## SHOOTING INTEGRATION

- Boss shooting is defined by shoot patterns
- Patterns may be composed or layered per phase
- All projectiles are spawned via the Projectile System

The Boss System does NOT manage projectile behavior.

---

## DAMAGE HANDLING

- Damage is applied via Collision System events
- Boss System updates HP or module HP
- Phase transitions may depend on HP thresholds

The Boss System MUST NOT resolve collisions.

---

## UI INTEGRATION

The Boss System exposes:

- current boss state
- normalized boss HP values

UI systems consume this data for boss health display.

---

## PERFORMANCE CONSTRAINTS

- Boss logic must be lightweight
- Phase evaluation must be deterministic
- Module count is limited and explicit

Boss encounters must remain predictable.

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- adaptive boss AI
- dynamic difficulty scaling
- player-targeted chasing behavior
- implicit phase transitions

---

## INTEGRATION NOTES

- Wave System triggers boss encounter start
- Enemy System may be paused during boss fights
- Projectile System handles all bullets
- Effect System handles boss visuals

Boss System operates as a scripted encounter controller.

---

## FINAL RULE

If a boss implementation:

- introduces decision-making
- reacts dynamically to player behavior
- embeds movement or shooting logic

It is incorrect and must be rejected.
