# DIRECTIVE 080 — DROP SYSTEM

## PURPOSE

Implement the Drop System as a deterministic reward and progression routing layer.

This directive introduces collectible drops that respond to enemy and boss destruction
without embedding combat or progression logic.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/drop-system.context.md
- docs/systems/enemy-system.context.md
- docs/systems/boss-system.context.md
- docs/systems/player-system.context.md
- docs/systems/collision-system.context.md

Load the following skill references:

- docs/skills/context7.md
- docs/skills/data-driven-design.md

---

## GOAL

Create a Drop System that:

- spawns collectible drops on explicit signals
- updates drop movement and lifetime deterministically
- routes collected rewards to the correct systems
- integrates cleanly into the core loop

---

## CONSTRAINTS

- Do NOT decide drop timing or rarity
- Do NOT apply combat effects
- Do NOT mix run-based and meta progression
- Do NOT allocate objects during update loops
- Drop behavior must be deterministic

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ DropSystem.ts

src/entities/
├─ Drop.ts

src/data/
├─ drops/
│  ├─ drop-types.ts
```

---

## DROP DATA MODEL

Define a drop data structure including:

- id
- dropType (coin | powerUp)
- subtype
- position
- lifetime
- value or effectDescriptor
- hitbox

The model MUST match the Drop System context.

---

## SPAWN INTEGRATION

The Drop System listens for events from:

- Enemy destruction
- Boss phase completion or defeat

Upon receiving a valid signal:

- spawn the configured drop
- do not alter drop configuration

---

## DROP MOVEMENT

Per update tick:

- Update drop position (simple drift)
- Optionally apply weak attraction to player
- Decrease lifetime
- Remove drop if expired or out of viewport

Attraction behavior MUST be capped and predictable.

---

## COLLECTION INTEGRATION

- Collision System emits collection events
- Drop System reacts to collection events

Upon collection:

- coins are routed to meta progression (stub)
- power-ups are routed to Player System

---

## PERFORMANCE REQUIREMENTS

- Drops must be pooled
- Drop count per wave is limited
- No per-frame memory allocation

---

## VALIDATION CHECKLIST

This directive is complete when:

- Drops spawn on enemy/boss destruction
- Drops move and expire correctly
- Player can collect drops
- Rewards are routed correctly
- No combat logic exists in Drop System

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- UI representation of rewards
- Persistent storage
- Balance tuning

---

## FINAL NOTE

The Drop System closes the gameplay reward loop.

If reward logic becomes implicit, mixed, or reactive,
it must be simplified.
