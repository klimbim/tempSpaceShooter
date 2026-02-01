# WAVE SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Wave System.

The Wave System is responsible for orchestrating combat encounters
by spawning enemies in scripted, deterministic waves.

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing wave logic

---

## SYSTEM ROLE

The Wave System acts as the **scenario controller** for a combat stage.

It:

- defines the order of waves
- controls when enemies appear
- determines when a wave starts and ends

The Wave System does NOT:

- control enemy behavior
- update enemies or projectiles
- apply damage
- handle collisions

---

## OWNERSHIP

The Wave System OWNS:

- wave definitions
- wave sequencing
- wave state (current, pending, completed)
- inter-wave timing

The Wave System DOES NOT OWN:

- enemy logic
- movement logic
- shooting logic
- drop logic

---

## WAVE DEFINITION (DATA-DRIVEN)

A wave is defined entirely by data.

Each wave definition includes:

- entryDelay
- spawnGroups
- endCondition
- rewardPolicy

No wave behavior may be hard-coded.

---

## SPAWN GROUPS

A spawn group defines how enemies are introduced.

Each spawn group includes:

- enemyType
- count
- spawnPattern
- movementPattern
- shootPattern
- spawnInterval

Spawn groups MAY:

- overlap in time
- start with offsets

Spawn groups MUST NOT:

- react dynamically to player state
- modify other spawn groups

---

## WAVE FLOW

Typical wave lifecycle:

1. Entry delay
2. Spawn groups activated
3. Enemies execute assigned patterns
4. End condition evaluated
5. Inter-wave pause
6. Next wave starts

All transitions MUST be explicit.

---

## END CONDITIONS

A wave ends when one of the following conditions is met:

- all spawned enemies are defeated
- a fixed duration expires
- all required enemies are defeated

End conditions MUST be deterministic.

---

## REWARD POLICY

The Wave System only signals reward opportunities.

It MAY:

- signal coin drop bonuses
- signal power-up eligibility

The Wave System MUST NOT:

- spawn drops directly
- decide specific drop types

Drop resolution belongs to the Drop System.

---

## PERFORMANCE CONSTRAINTS

- Wave evaluation must be lightweight
- No per-frame scanning of large enemy lists
- No dynamic restructuring of wave data

Wave state transitions should be event-driven.

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- random wave generation
- adaptive difficulty scaling
- enemy AI decisions inside waves
- time-based guessing of wave completion

---

## INTEGRATION NOTES

- Enemy System spawns enemies on request
- Movement Patterns define enemy paths
- Projectile System handles firing via shoot patterns

The Wave System remains purely declarative.

---

## FINAL RULE

If a wave implementation:

- embeds behavior logic
- reacts to player performance
- hides transition rules

It is incorrect and must be rejected.
