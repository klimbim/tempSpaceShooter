# PROJECTILE SYSTEM — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for the Projectile System.

It exists to:

- constrain AI implementation
- define system responsibilities
- prevent logic leakage into other systems

This file MUST be treated as read-only by AI agents.

---

## SYSTEM ROLE

The Projectile System is responsible for:

- managing all projectiles (player and enemy)
- updating projectile movement deterministically
- handling projectile lifetime
- exposing projectile hitboxes for collision checks

The Projectile System is NOT responsible for:

- collision detection
- damage resolution
- visual effects beyond basic representation
- gameplay decisions

---

## OWNERSHIP

The Projectile System OWNS:

- projectile data
- projectile pooling
- projectile spawn and despawn
- projectile movement updates

The Projectile System DOES NOT OWN:

- enemy logic
- player logic
- wave logic
- collision logic
- effects or explosions

---

## PROJECTILE DEFINITION

Each projectile is defined purely by data.

Mandatory fields:

- position
- direction
- speed
- movementPattern
- lifetime
- damage
- damageType
- owner (player | enemy)
- hitbox

Optional fields:

- visualVariant
- trailVariant

Projectiles MUST NOT contain behavior logic.

---

## MOVEMENT RULES

- Projectile movement MUST be deterministic
- Movement is evaluated as a function of time
- Movement patterns are parameterized data

Allowed movement patterns:

- linear
- sine-offset
- spiral
- limited homing

Movement patterns:

- must be reusable
- must not depend on external state
- must not query other systems

---

## LIFETIME MANAGEMENT

A projectile is removed when:

- lifetime expires
- the projectile hitbox center exits the gameplay viewport
- a collision event marks it as consumed

Upon collision:

- the projectile hitbox MUST be removed immediately
- the projectile MUST NOT participate in further updates or collisions

Logical removal MUST occur in the same frame the hit is registered.

Visual effects may continue independently.

---

## COLLISION INTEGRATION

The Projectile System:

- exposes projectile hitboxes
- listens for collision result events

The Projectile System MUST NOT:

- detect collisions
- apply damage
- decide hit outcomes

Upon receiving a hit event:

- the projectile is flagged for removal

---

## PERFORMANCE CONSTRAINTS

- Projectile count is expected to be the highest among entities
- Object pooling is mandatory
- No memory allocation during update
- No dynamic creation of movement logic

All projectiles share a unified update path.

---

## PLAYER VS ENEMY PROJECTILES

Player and enemy projectiles:

- use the same system
- use the same data structures
- differ only by `owner` and configuration

No branching logic based on owner is allowed inside the system.

---

## DATA-DRIVEN SPAWN

The Projectile System does not decide when to spawn projectiles.

Projectiles are spawned via explicit requests from:

- Player System
- Enemy System
- Boss System

Spawn requests MUST provide full projectile configuration.

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- projectile-to-projectile interaction
- projectile blocking or canceling other projectiles
- random trajectory changes
- dynamic logic injection
- physics-based behavior
- collision side effects

Projectile-to-projectile interaction is forbidden unless implemented as a separate, explicit system (e.g. area effects or shields), which is out of scope for the current architecture.

---

## INTEGRATION NOTES

- Projectile System is updated every frame
- Collision System queries projectile hitboxes
- Effect System reacts to projectile removal

The Projectile System must remain isolated and predictable.

---

## FINAL RULE

If an implementation choice introduces:

- hidden state
- system coupling
- non-determinism

That implementation is incorrect and must be rejected.
