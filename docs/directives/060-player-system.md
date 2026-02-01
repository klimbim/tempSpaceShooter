# DIRECTIVE 060 — PLAYER SYSTEM

## PURPOSE

Implement the Player System as an input-driven, deterministic entity controller.

This directive introduces the player ship, movement intent, and player weapon firing,
without yet resolving collisions or damage.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/player-system.context.md
- docs/systems/projectile-system.context.md
- docs/systems/movement-patterns.context.md

Load the following skill references:

- docs/skills/context7.md
- docs/skills/deterministic-systems.md
- docs/skills/webgl-performance.md

---

## GOAL

Create a Player System that:

- updates player movement from abstract input intent
- fires player projectiles automatically
- supports run-based weapon upgrades (stubbed)
- integrates cleanly into the core loop

No collision resolution or damage handling is implemented yet.

---

## CONSTRAINTS

- Do NOT read raw input events
- Do NOT implement collision detection
- Do NOT apply damage or shield logic
- Do NOT allocate objects during update loops
- Player behavior must be deterministic

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ PlayerSystem.ts

src/entities/
├─ Player.ts

src/input/
├─ InputSystem.ts
```

---

## INPUT ABSTRACTION

Implement an InputSystem that:

- converts device input into abstract intent
- exposes:

  - targetPosition
  - fireActive
  - specialActive

The Player System consumes intent only.

---

## PLAYER DATA MODEL

Define player data including:

- position
- velocity
- maxSpeed
- acceleration
- weaponState
- hitbox (placeholder)

The model MUST match the player system context.

---

## MOVEMENT UPDATE

Per update tick:

- Compute desired direction toward targetPosition
- Accelerate player toward direction
- Clamp speed to maxSpeed
- Update position deterministically

Visual tilt is optional and non-functional.

---

## WEAPON FIRING

- Player fires while fireActive is true
- Fire rate is fixed and deterministic
- Projectiles are spawned via Projectile System

Weapon upgrades are stubbed as data changes only.

---

## PERFORMANCE REQUIREMENTS

- Player update must be lightweight
- No dynamic weapon logic generation
- No per-frame allocations

---

## VALIDATION CHECKLIST

This directive is complete when:

- Player can move via abstract input
- Player fires projectiles continuously
- Player behavior is deterministic
- No collision or damage logic exists

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Collision resolution
- Damage and shield logic
- Power-up collection
- UI and HUD

---

## FINAL NOTE

The Player System must feel responsive and predictable.

If player behavior becomes implicit or reactive,
it must be simplified.
