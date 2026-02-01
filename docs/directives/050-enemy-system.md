# DIRECTIVE 050 — ENEMY SYSTEM

## PURPOSE

Implement the Enemy System as a deterministic executor of scripted behavior.

This directive introduces enemies as active entities with HP, movement, and shooting,
fully controlled by wave data and predefined patterns.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/enemy-system.context.md
- docs/systems/wave-system.context.md
- docs/systems/movement-patterns.context.md
- docs/systems/projectile-system.context.md

Load the following skill references:

- docs/skills/data-driven-design.md
- docs/skills/context7.md
- docs/skills/deterministic-systems.md
- docs/skills/bullet-hell-design.md

---

## GOAL

Create an Enemy System that:

- spawns enemies from Wave System requests
- updates enemy movement deterministically
- fires projectiles using predefined shoot patterns
- manages enemy HP and destruction

No player interaction is implemented yet.

---

## CONSTRAINTS

- Do NOT introduce AI decision-making
- Do NOT query player state
- Do NOT implement collision detection
- Do NOT allocate objects during update loops
- Enemy behavior must be fully data-driven

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ EnemySystem.ts

src/entities/
├─ Enemy.ts

src/data/
├─ enemies/
│  ├─ enemy-types.ts
```

---

## ENEMY DATA MODEL

Define an enemy data structure including:

- id
- position
- hp
- hitbox
- movementPattern
- shootPattern
- phase (optional)

The model MUST match the enemy system context.

---

## SPAWN INTERFACE

The Enemy System MUST expose a spawn method that:

- accepts full enemy configuration
- does not infer or modify behavior
- returns no value

Enemies are passive after spawn.

---

## MOVEMENT UPDATE

Per update tick:

- Advance enemy time
- Apply movement pattern
- Update position deterministically

Movement logic must delegate to MovementSystem.

---

## SHOOTING UPDATE

- Shooting behavior is defined by shootPattern data
- Enemy System requests projectile spawns
- Shooting timing is deterministic

Enemy System does not manage projectile logic.

---

## HP AND DESTRUCTION

- Enemy HP is reduced via hit events (placeholder)
- When HP reaches zero:

  - enemy is marked destroyed
  - destruction event is emitted

Actual collision integration comes later.

---

## PERFORMANCE REQUIREMENTS

- Enemy updates must be lightweight
- No dynamic behavior generation
- Enemy count per wave is predictable

---

## VALIDATION CHECKLIST

This directive is complete when:

- Enemies spawn via Wave System
- Enemies move according to patterns
- Enemies fire projectiles deterministically
- Enemy destruction is handled correctly
- No AI or player logic exists

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Player system
- Collision detection
- Drop spawning
- Boss logic

---

## FINAL NOTE

Enemies are scripted actors, not thinkers.

If enemy logic becomes reactive or stateful beyond definition,
it must be simplified.
