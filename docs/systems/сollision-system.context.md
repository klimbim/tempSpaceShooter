# COLLISION SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Collision System.

The Collision System is the single source of truth for hit detection and hit event generation.

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing collision logic

---

## SYSTEM ROLE

The Collision System is responsible for:

- detecting intersections between hitboxes
- determining valid hit pairs
- emitting deterministic hit events

The Collision System does NOT:

- move entities
- apply damage values
- remove entities directly
- trigger visual effects

---

## OWNERSHIP

The Collision System OWNS:

- hitbox definitions and queries
- collision rules between entity categories
- hit event emission

The Collision System DOES NOT OWN:

- entity lifecycle
- HP or shield logic
- projectile behavior
- visual feedback

---

## HITBOX MODEL

Hitboxes are defined independently from visuals.

Each hitbox includes:

- ownerId
- ownerType (player | enemy | boss | projectile)
- shape (circle | rectangle)
- size parameters
- offset relative to owner position

Hitboxes MUST:

- be simple shapes
- be cheap to evaluate

---

## COLLISION PAIRS (RULES)

Allowed collision pairs:

- player <-> enemy projectile
- player <-> enemy / boss body
- enemy / boss <-> player projectile

Forbidden collision pairs:

- projectile <-> projectile
- enemy <-> enemy
- enemy <-> boss
- player <-> player

Exceptions require a separate, explicit system and are out of scope.

---

## COLLISION FLOW

Per update tick:

1. Gather active hitboxes
2. Evaluate allowed collision pairs
3. Detect intersections
4. Emit hit events

Collision evaluation MUST be deterministic and order-independent.

---

## HIT EVENTS

A hit event includes:

- sourceId
- sourceType
- targetId
- targetType
- damageType
- timestamp (frame or time)

Hit events:

- are emitted once per valid intersection
- do not apply damage directly

---

## DE-DUPLICATION AND SAFETY

Rules:

- A projectile may generate at most one hit event
- Hitboxes marked as inactive MUST NOT be evaluated
- Consumed projectiles MUST be ignored immediately

This prevents:

- multi-hit artifacts
- hitbox sticking
- frame-repeat hits

---

## VIEWPORT HANDLING

- Hitboxes outside the gameplay viewport are ignored
- Viewport checks occur before collision evaluation

---

## PERFORMANCE CONSTRAINTS

- Collision checks must scale predictably
- Broad-phase optimizations are allowed
- No allocations during collision checks

Simple spatial partitioning MAY be used.

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- physics simulation
- continuous collision resolution
- collision-based movement response
- collision logic embedded in other systems

---

## INTEGRATION NOTES

- Projectile System provides projectile hitboxes
- Enemy and Boss Systems provide body hitboxes
- Player System provides player hitbox
- Effect and Damage Systems consume hit events

The Collision System emits events only.

---

## FINAL RULE

If collision logic:

- applies damage
- removes entities
- depends on update order

It is incorrect and must be rejected.
