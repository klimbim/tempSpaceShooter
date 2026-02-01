# DIRECTIVE 010 — CORE LOOP

## PURPOSE

Establish the core execution loop and system update order for the game.

This directive defines how time flows, how systems are updated, and how events are dispatched.
It creates the stable backbone that all gameplay systems will plug into.

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

Load the following skill references:

- docs/skills/context7.md
- docs/skills/deterministic-systems.md

---

## GOAL

Create a deterministic core loop that:

- updates all systems in a fixed, explicit order
- separates update logic from rendering
- provides a central event dispatch mechanism
- introduces no gameplay logic yet

---

## CONSTRAINTS

- Do NOT introduce gameplay behavior
- Do NOT introduce rendering logic beyond what already exists
- Do NOT introduce ECS frameworks
- Do NOT introduce randomness
- Keep the loop explicit and readable

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/core/
├─ Engine.ts
├─ Time.ts
├─ EventBus.ts
```

Existing files may be extended but not refactored heavily.

---

## CORE LOOP STRUCTURE

The core loop MUST follow this high-level order:

1. Time update (delta calculation)
2. Input intent update (placeholder only)
3. System updates (ordered, deterministic)
4. Event dispatch processing
5. Rendering

This order MUST remain consistent.

---

## SYSTEM UPDATE ORDER (PLACEHOLDER)

Define an explicit system update pipeline, even if systems are not yet implemented:

1. Player System (placeholder)
2. Enemy System (placeholder)
3. Projectile System (placeholder)
4. Collision System (placeholder)
5. Drop System (placeholder)

These placeholders establish future integration points.

---

## EVENT BUS REQUIREMENTS

- Centralized publish/subscribe mechanism
- No direct system-to-system calls
- Events are simple data objects
- Event dispatch is deterministic per frame

The EventBus MUST NOT:

- contain game logic
- mutate system state directly

---

## TIME MANAGEMENT

- Time.ts provides:

  - deltaTime
  - elapsedTime

- Delta time MUST be capped to avoid spikes
- Time calculations MUST be frame-rate independent

---

## VALIDATION CHECKLIST

This directive is complete when:

- The game runs with a stable update loop
- The update order is explicit and readable
- EventBus exists and can emit events
- No gameplay behavior is implemented
- Future systems have clear integration points

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Player input handling
- Enemy spawning
- Projectiles
- Collisions
- UI

---

## FINAL NOTE

This core loop is the backbone of the entire project.

If a change complicates the loop or hides execution order,
it must be rejected.
