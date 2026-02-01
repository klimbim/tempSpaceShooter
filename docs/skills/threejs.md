# SKILL — THREE.JS

## INTENT

Enforce a disciplined, minimal, and predictable way of working with Three.js.

This skill prevents tutorial-style usage and promotes scene stability,
clear ownership, and explicit lifecycle control.

---

## CORE PRINCIPLES

- Scene is a data graph, not a logic container
- Objects are created rarely and reused often
- Updates are explicit and centralized
- Visuals never drive gameplay logic

Three.js is a renderer, not a game engine.

---

## PREFERRED PATTERNS

- One Scene, one Camera, one Renderer
- Explicit creation and disposal of objects
- Stable object hierarchies
- Update transforms and uniforms, not topology
- Decouple visuals from simulation state

Prefer simple meshes and materials over complex abstractions.

---

## AVOID

- Creating or destroying meshes per frame
- Attaching gameplay logic to Three.js objects
- Using scene traversal for game logic
- Implicit side effects inside render calls
- Copying patterns from tutorials without evaluation

If a visual object owns logic, it is incorrect.

---

## DECISION RULES

When choosing an approach:

- Prefer fewer objects over cleaner hierarchies
- Prefer explicit updates over callbacks
- Prefer manual control over convenience helpers

If ownership or lifecycle is unclear, refactor.

---

## WHEN TO USE

- Renderer setup and integration
- Camera behavior and constraints
- Visual representation of entities

Avoid using this skill for pure gameplay systems.

---

## GOAL

Keep the rendering layer stable, performant, and predictable.

Visual fidelity must never compromise control or determinism.
