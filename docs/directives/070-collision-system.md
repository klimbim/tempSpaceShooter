# DIRECTIVE 070 — COLLISION SYSTEM

## PURPOSE

Implement the Collision System as the single source of truth for hit detection.

This directive connects projectiles, enemies, bosses, and the player
through deterministic hit event generation.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/collision-system.context.md
- docs/systems/projectile-system.context.md
- docs/systems/enemy-system.context.md
- docs/systems/player-system.context.md
- docs/systems/boss-system.context.md

Load the following skill references:

- docs/skills/context7.md
- docs/skills/webgl-performance.md
- docs/skills/deterministic-systems.md

---

## GOAL

Create a Collision System that:

- evaluates hitbox intersections deterministically
- emits hit events via EventBus
- enforces allowed and forbidden collision pairs
- integrates cleanly into the core loop

---

## CONSTRAINTS

- Do NOT apply damage directly
- Do NOT remove entities directly
- Do NOT perform physics simulation
- Do NOT allocate objects during collision checks
- Collision logic must be order-independent

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ CollisionSystem.ts

src/utils/
├─ SpatialGrid.ts (optional)
```

---

## HITBOX REGISTRATION

Implement a hitbox registry that:

- receives active hitboxes from systems each frame
- ignores inactive or consumed hitboxes
- does not retain references across frames

Hitboxes are evaluated per-frame only.

---

## COLLISION PAIR FILTERING

Enforce collision rules strictly:

Allowed:

- player ↔ enemy projectile
- player ↔ enemy / boss body
- enemy / boss ↔ player projectile

Forbidden:

- projectile ↔ projectile
- enemy ↔ enemy
- enemy ↔ boss

Forbidden pairs must never be evaluated.

---

## COLLISION EVALUATION

Per update tick:

1. Gather hitboxes
2. Apply broad-phase filtering (if implemented)
3. Evaluate allowed collision pairs
4. Detect intersections
5. Emit hit events

Evaluation must be deterministic and frame-order independent.

---

## HIT EVENT EMISSION

Each hit event must include:

- sourceId
- sourceType
- targetId
- targetType
- damageType

Events are emitted once per valid collision.

---

## SAFETY RULES

- A projectile may emit only one hit event
- Consumed projectiles must be ignored immediately
- Hitboxes outside viewport are ignored

These rules prevent multi-hit and sticking bugs.

---

## PERFORMANCE REQUIREMENTS

- Collision checks must scale predictably
- Broad-phase optimization is allowed
- No per-frame memory allocation

---

## VALIDATION CHECKLIST

This directive is complete when:

- Collisions generate hit events correctly
- Forbidden collision pairs never trigger
- Projectiles generate only one hit
- Collision order does not affect outcome

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Damage application
- HP or shield reduction
- Visual hit effects
- Drop spawning

---

## FINAL NOTE

The Collision System is the arbiter of truth for hits.

If collision logic leaks into other systems or becomes stateful,
it must be rejected.
