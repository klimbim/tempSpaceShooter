# HARD CONSTRAINTS (AI FOUNDATION)

## PURPOSE OF THIS DOCUMENT

This document defines hard, non-negotiable constraints for the project.

These constraints exist to:

- limit solution space for AI agents
- protect performance and scope
- prevent architectural overreach

This file:

- MUST be treated as read-only
- MUST be loaded for all directives and system implementations

---

## PLATFORM CONSTRAINTS

- Primary target: Desktop (PC / Mac)
- Input: Mouse + Keyboard
- Mobile support: optional, via input abstraction only

Mobile-specific features MUST NOT influence core gameplay design.

---

## PERFORMANCE CONSTRAINTS

- Target frame rate: stable 60 FPS
- Object count on screen: ~30–100 active entities
- Projectiles are expected to be the most frequent objects

Mandatory rules:

- No memory allocations in update loops
- Object pooling REQUIRED for:

  - projectiles
  - explosions
  - temporary effects

Visual effects MUST degrade gracefully if needed.

---

## RENDERING CONSTRAINTS

- Top-down view
- Orthographic camera
- Fixed gameplay viewport (no camera scrolling)
- Camera movement allowed only for:

  - screen shake
  - intro / outro motion

Depth is used only for layering, not gameplay.

---

## GAMEPLAY CONSTRAINTS

- Single-player only
- No multiplayer or networking considerations
- No procedural or random wave generation
- No emergent AI behavior

Enemies:

- Do not collide with each other
- Always have explicit HP
- Are active only when visible on screen

---

## PROGRESSION CONSTRAINTS

- Two progression layers only:

  - Meta progression (coins, between runs)
  - Run progression (power-ups, within a run)

Mixing these layers is forbidden.

- On player death:

  - run progression resets completely
  - meta progression persists

---

## TECHNICAL SCOPE LIMITS

The following are explicitly OUT OF SCOPE:

- Physics engines
- Procedural generation systems
- Advanced AI or decision trees
- Multiplayer architecture
- Save/load systems beyond simple progression

Any feature requiring these is considered invalid.

---

## CHANGE POLICY

If a requested change:

- increases system coupling
- increases runtime complexity
- increases AI decision-making

The change MUST be rejected or redesigned.

---

## FINAL RULE

Constraints override preferences.

If a design or implementation idea conflicts with any constraint in this document,
it MUST NOT be implemented.
