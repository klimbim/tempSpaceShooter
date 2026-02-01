# MOVEMENT PATTERNS — SYSTEM CONTEXT

## PURPOSE

This document defines the authoritative context for Movement Patterns.

Movement Patterns are a shared, data-driven layer used by:

- Projectile System
- Enemy System
- Boss System

This file:

- MUST be treated as read-only by AI agents
- MUST be loaded by any directive implementing movement logic

---

## SYSTEM ROLE

Movement Patterns define **how entities move over time**.

They:

- are pure functions of time and parameters
- produce positional offsets or direction modifiers
- contain no gameplay logic

Movement Patterns do NOT:

- spawn entities
- apply damage
- query other systems
- react to collisions

---

## DESIGN PRINCIPLES

- Data-driven over hard-coded behavior
- Deterministic and reproducible
- Readable motion over complex motion
- Shared implementation across systems

If a pattern cannot be described clearly, it is invalid.

---

## INPUTS

Each movement pattern receives:

- basePosition (Vector2)
- direction (Vector2)
- speed (number)
- time (number, seconds since spawn)
- parameters (pattern-specific data)

Patterns MUST NOT depend on:

- frame count
- random values
- external state

---

## OUTPUTS

Patterns output one of the following:

- position offset
- direction offset

They MUST NOT directly modify entity state.

---

## SUPPORTED BASE PATTERNS

### 1. Linear

Description:

- Constant movement in a single direction

Parameters:

- none

Use cases:

- basic bullets
- simple enemy entry

---

### 2. Sine Offset (Zigzag)

Description:

- Oscillating movement along a perpendicular axis

Parameters:

- amplitude
- frequency

Use cases:

- zigzag enemies
- wave bullets

---

### 3. Infinity (Figure-8)

Description:

- Smooth figure-eight trajectory

Parameters:

- amplitudeX
- amplitudeY
- frequency

Use cases:

- elite enemies
- boss sub-patterns

---

### 4. Spiral

Description:

- Rotational movement around forward axis

Parameters:

- angularSpeed

Use cases:

- boss bullet patterns
- visual pressure zones

---

### 5. Lane Switch

Description:

- Discrete horizontal movement between lanes

Parameters:

- laneCount
- switchInterval

Use cases:

- formation enemies
- readable horizontal pressure

---

### 6. Limited Homing

Description:

- Gradual steering toward a target direction

Parameters:

- turnRate
- maxAngle

Constraints:

- MUST NOT track targets dynamically
- target direction is sampled once at spawn

Use cases:

- rockets
- special enemy attacks

---

## COMPOSITION RULES

Movement Patterns MAY be composed sequentially:

- entry pattern
- active pattern
- exit pattern

Composition MUST be explicit in data.

Implicit blending is forbidden.

---

## TIME HANDLING

- Time is measured from entity spawn
- Time resets per entity
- Patterns MUST behave consistently regardless of frame rate

---

## PERFORMANCE CONSTRAINTS

- Patterns must be allocation-free
- No dynamic function creation
- All math must be predictable and bounded

---

## FORBIDDEN BEHAVIOR

The following are strictly forbidden:

- random noise-based movement
- physics simulation
- collision-aware steering
- querying player or enemy state

---

## INTEGRATION NOTES

- Projectile System applies movement patterns per update
- Enemy System assigns patterns via wave data
- Boss System switches patterns via phase definitions

Movement Patterns are a shared language across systems.

---

## FINAL RULE

If a movement pattern:

- reduces readability
- introduces hidden state
- depends on external data

It must not be implemented.
