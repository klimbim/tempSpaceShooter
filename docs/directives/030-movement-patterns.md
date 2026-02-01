# DIRECTIVE 030 — MOVEMENT PATTERNS

## PURPOSE

Implement the Movement Patterns layer as a reusable, deterministic module.

This directive formalizes all movement logic used by:

- projectiles
- enemies
- bosses

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/movement-patterns.context.md
- docs/systems/projectile-system.context.md

Load the following skill references:

- docs/skills/data-driven-design.md
- docs/skills/context7.md
- docs/skills/deterministic-systems.md

---

## GOAL

Create a Movement Patterns module that:

- exposes deterministic movement functions
- is fully data-driven
- can be shared across systems
- contains no gameplay logic

---

## CONSTRAINTS

- Use TypeScript pragmatically
- Do NOT query external state
- Do NOT allocate objects during updates
- Do NOT embed logic into entities

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ MovementSystem.ts

src/utils/
├─ Math.ts
```

---

## PATTERN INTERFACE

Define a minimal pattern interface that:

- receives base position, direction, speed, time
- receives pattern-specific parameters
- returns position or direction offset

Patterns must be selectable by id or name.

---

## REQUIRED PATTERNS

Implement the following patterns:

1. Linear
2. Sine Offset (zigzag)
3. Infinity (figure-8)
4. Spiral
5. Limited Homing

Each pattern must strictly follow the system context definition.

---

## COMPOSITION SUPPORT

Movement patterns must support explicit composition:

- entry pattern
- active pattern
- exit pattern

Composition must be data-defined and explicit.

---

## INTEGRATION

- Projectile System uses MovementSystem for position updates
- Future Enemy and Boss Systems will reuse the same patterns

MovementSystem must not depend on any specific system.

---

## VALIDATION CHECKLIST

This directive is complete when:

- All required patterns exist
- Patterns are deterministic and reproducible
- No allocations occur during updates
- Patterns can be reused by multiple systems
- No gameplay logic exists inside patterns

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Enemy behavior
- Boss logic
- Wave sequencing
- Collision detection

---

## FINAL NOTE

Movement Patterns define the "language of motion" in the game.

If a pattern reduces readability or depends on hidden state,
it must be rejected.
