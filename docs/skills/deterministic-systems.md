# SKILL — DETERMINISTIC SYSTEMS

## INTENT

Enforce deterministic behavior across all gameplay systems.

This skill ensures that the same inputs always produce the same outputs,
independent of frame rate, update order, or platform.

---

## CORE PRINCIPLES

- Same state + same input = same result
- Explicit update order over implicit dependencies
- Time-based logic over frame-based logic
- Events over direct calls

Determinism is required for fairness and debuggability.

---

## PREFERRED PATTERNS

- Fixed update sequences
- Delta-time–based calculations
- Stateless or explicitly reset state machines
- Event-driven reactions

All transitions must be explicit and observable.

---

## AVOID

- Hidden timers or implicit cooldowns
- Randomness without a seeded source
- Logic depending on iteration order
- Side effects during iteration
- Frame-count–based behavior

---

## DECISION RULES

When designing system logic:

- Prefer explicit state transitions
- Prefer events to trigger effects
- Prefer data-defined timing over code-defined timing

If behavior varies between runs, it is incorrect.

---

## WHEN TO USE

- Core loop
- Collision and projectile systems
- Wave sequencing and spawning

Avoid using for purely visual or cosmetic systems.

---

## GOAL

Guarantee fairness, predictability, and stable AI-assisted development.

Determinism is more important than realism.
