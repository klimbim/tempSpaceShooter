# TECH STACK (AI FOUNDATION)

## PURPOSE OF THIS DOCUMENT

This document defines the approved technical stack and rendering approach.

It exists to:

- constrain implementation choices
- ensure consistency across systems
- prevent unnecessary experimentation

This file:

- MUST be treated as read-only
- MUST be loaded for all rendering- and engine-related directives

---

## CORE TECHNOLOGY

### Rendering Engine

- **Three.js** is the primary rendering engine
- Rendering backend: **WebGL**
- Future migration path to **WebGPU** is allowed but NOT required

Rationale:

- Mature ecosystem
- Stable performance on desktop
- Strong support for custom shaders and postprocessing
- Clear separation between scene, camera, and rendering loop

---

## WHY NOT PIXI OR PURE 2D ENGINES

Pixi.js and similar 2D engines are explicitly NOT used because:

- Limited postprocessing pipeline
- Less flexible shader composition
- Weaker camera and depth abstractions

The project requires:

- screen-space effects
- distortion and damage feedback
- pseudo-3D motion and depth layering

These are better served by Three.js.

---

## CAMERA SETUP

- Camera type: **Orthographic**
- View: **Top-down**
- Gameplay viewport is fixed

Camera behavior:

- No scrolling
- No zoom during gameplay
- Camera motion allowed only for:

  - screen shake
  - intro / outro motion
  - acceleration feedback

Camera movement MUST NOT affect gameplay logic.

---

## SCENE STRUCTURE

The scene graph is used ONLY for rendering.

Rules:

- Scene graph depth must be shallow
- No gameplay logic inside scene nodes
- Scene objects reflect game state, not control it

All gameplay data lives outside the Three.js scene.

---

## UPDATE LOOP

- Single global update loop
- Fixed timestep preferred
- Rendering and logic updates are separated conceptually

Rules:

- No allocations inside update loops
- No dynamic scene graph reconstruction per frame

---

## ASSET PIPELINE

### Graphics

- 2D sprites rendered on planes or billboards
- Assets are authored as 2D textures
- Texture atlases are preferred

### Guidelines

- Consistent scale reference across all assets
- Visual center aligns with logical center
- Hitboxes are defined independently from visuals

---

## POSTPROCESSING

Postprocessing is a core visual feature.

Allowed effects:

- bloom / glow
- screen shake
- distortion
- damage overlays (cracks, noise)

Rules:

- Postprocessing effects are screen-space only
- Effects MUST NOT affect gameplay state
- Effects must degrade gracefully if needed

---

## INPUT ABSTRACTION

Input is abstracted from gameplay logic.

- Mouse, keyboard, and touch inputs map to intent
- Gameplay systems consume intent, not raw input

This enables optional mobile support without redesigning gameplay.

---

## DATA-DRIVEN CONFIGURATION

- Gameplay configuration stored as data objects
- No hard-coded wave or pattern logic
- Systems interpret configuration, not embed it

This aligns with data-driven principles and enables rapid iteration.

---

## FINAL RULE

If a technology choice or implementation detail:

- increases coupling
- complicates the pipeline
- introduces unnecessary abstraction

It MUST be rejected in favor of the simpler solution.
