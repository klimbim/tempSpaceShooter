# DIRECTIVE 020 — PROJECTILE SYSTEM

## PURPOSE

Implement the core Projectile System according to the established architecture.

This directive introduces the first gameplay system and validates:

- the core loop integration
- deterministic updates
- data-driven behavior

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md
- docs/foundation/tech-stack.md

Load the following system contexts:

- docs/systems/projectile-system.context.md
- docs/systems/movement-patterns.context.md
- docs/systems/collision-system.context.md

Load the following skill references:

- docs/skills/context7.md
- docs/skills/data-driven-design.md
- docs/skills/deterministic-systems.md
- docs/skills/webgl-performance.md

---

## GOAL

Implement a deterministic, pooled Projectile System that:

- spawns projectiles on explicit requests
- updates projectile movement using Movement Patterns
- manages projectile lifetime and viewport removal
- exposes hitboxes to the Collision System

No enemies or player logic are implemented yet.

---

## CONSTRAINTS

- Use TypeScript pragmatically (no advanced typing)
- Do NOT implement collision detection
- Do NOT apply damage
- Do NOT add randomness
- Do NOT allocate objects during update loops

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ ProjectileSystem.ts

src/entities/
├─ Projectile.ts

src/utils/
├─ Pool.ts

src/data/
├─ projectiles/ (optional placeholder)
```

---

## PROJECTILE DATA MODEL

Define a simple data structure for projectiles including:

- position
- direction
- speed
- lifetime
- owner
- movementPattern
- hitbox

The data model MUST match the projectile system context.

---

## SPAWN INTERFACE

The Projectile System MUST expose a spawn method that:

- accepts a full projectile configuration
- does not infer or modify configuration
- returns no value

Spawn requests are expected from future systems only.

---

## UPDATE LOGIC

Per update tick:

1. Iterate active projectiles
2. Advance time and apply movement pattern
3. Update position deterministically
4. Decrease lifetime
5. Mark projectile for removal if:

   - lifetime expired
   - hitbox center exits viewport
   - projectile marked consumed by collision events

No sorting or dynamic collections are allowed during update.

---

## POOLING REQUIREMENTS

- All projectiles must be pooled
- Pool growth must be explicit and bounded
- No new Projectile instances created during gameplay

---

## COLLISION INTEGRATION

- Expose active projectile hitboxes to the Collision System
- Listen for hit events related to projectiles
- Immediately mark consumed projectiles as inactive

The Projectile System MUST NOT query collision state.

---

## VALIDATION CHECKLIST

This directive is complete when:

- Projectiles can be spawned manually (test hook)
- Projectiles move deterministically
- Projectiles are removed correctly on lifetime/viewport exit
- No memory allocations occur in the update loop
- Projectile-to-projectile interaction does not exist

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Enemy spawning
- Player weapons
- Visual effects
- Damage application

---

## FINAL NOTE

This is the first real gameplay system.

If the implementation introduces coupling, hidden state, or non-determinism,
it must be simplified.
