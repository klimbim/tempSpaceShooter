# CORE PRINCIPLES (AI FOUNDATION)

## PURPOSE OF THIS DOCUMENT

This document defines non-negotiable engineering and design principles.

It exists to:

- constrain AI behavior
- prevent architectural drift
- enforce consistency across all systems

This file:

- MUST be treated as read-only
- MUST be loaded for all system and directive execution

---

## PRINCIPLE 1 — DATA OVER CODE

Gameplay behavior MUST be expressed as data whenever possible.

- Enemy behavior is described, not hard-coded
- Wave structure is defined by configuration
- Movement and shooting patterns are parameterized

Code exists to:

- interpret data
- execute deterministic logic

If behavior requires frequent changes, it MUST be data-driven.

---

## PRINCIPLE 2 — SYSTEMS OVER OBJECTS

The game is composed of independent systems, not smart objects.

- Systems own logic
- Entities are passive data containers
- No entity contains decision-making logic

Objects MUST NOT:

- update themselves
- reference other systems directly
- control game flow

All updates happen inside systems.

---

## PRINCIPLE 3 — DETERMINISTIC GAMEPLAY

All gameplay-relevant behavior MUST be deterministic.

- No randomness affecting outcomes
- No frame-dependent logic
- Same inputs produce the same results

Randomness MAY be used only for:

- cosmetic variation
- non-gameplay visuals

---

## PRINCIPLE 4 — SEPARATION OF LOGIC AND VISUALS

Gameplay logic and rendering MUST be strictly separated.

- Logic operates on abstract data
- Visuals react to state changes
- Effects NEVER influence gameplay state

Visual elements MAY outlive their logical entities.

---

## PRINCIPLE 5 — EXPLICIT STATE OVER IMPLICIT BEHAVIOR

All meaningful state MUST be explicit.

- Phases are defined, not inferred
- Transitions are declared, not guessed
- Conditions are evaluated, not assumed

Hidden or implicit behavior is forbidden.

---

## PRINCIPLE 6 — PERFORMANCE FIRST

Performance stability is a core feature.

- No allocations in update loops
- Object pooling is mandatory for projectiles and effects
- Systems must scale predictably

Visual quality MUST NOT compromise performance.

---

## PRINCIPLE 7 — READABILITY OVER COMPLEXITY

Gameplay clarity takes precedence over complexity.

- Fewer patterns, clearly communicated
- Fewer mechanics, well-explained
- Fewer exceptions, consistent rules

If a mechanic requires explanation, it is likely incorrect.

---

## PRINCIPLE 8 — CONTROLLED SCOPE

Features MUST be added only when required by gameplay.

Forbidden patterns:

- premature generalization
- speculative systems
- feature creep

The simplest working solution is preferred.

---

## ANTI-PATTERNS (STRICTLY FORBIDDEN)

The following are NOT allowed:

- Smart enemies with decision trees
- Random wave generation
- Physics-driven gameplay
- Tight coupling between systems
- Hidden side effects in updates

---

## FINAL RULE

If an implementation choice violates any principle in this document,
that implementation is incorrect.

When in doubt:

- choose simplicity
- choose clarity
- choose determinism
