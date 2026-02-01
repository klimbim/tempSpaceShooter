# Visual State Schema

Visual State is a **derived representation** of Game State for rendering.

It exists to:

- decouple gameplay from graphics
- allow interpolation and degradation
- prevent logic from leaking into rendering

---

## Core Rules

- Visual State is derived from Game State
- Visual State is never authoritative
- Gameplay systems must never read Visual State

---

## Visual State Characteristics

Visual State:

- may lag behind Game State
- may interpolate values
- may omit details
- may be rebuilt at any time

Loss of Visual State must not affect gameplay.

---

## Common Visual State Fields

Visual State may include:

- position (interpolated)
- rotation (interpolated)
- scale
- frameIndex
- animationProgress
- glowIntensity
- shieldOpacity
- engineThrust
- destructionProgress

This list is not exhaustive.

---

## Explicit Non-Responsibilities

Visual State must not:

- store HP
- store damage
- store collision data
- store AI decisions
- trigger gameplay events

---

## Lifecycle

Visual State:

- is created when entity becomes visible
- is updated every frame
- is destroyed when entity is no longer visible

Visual State lifecycle must not affect entity lifecycle.

---

## Failure Handling

If Visual State:

- is missing
- is corrupted
- is delayed

Gameplay must continue unaffected.
