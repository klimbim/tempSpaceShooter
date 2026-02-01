# DIRECTIVE 001 — INIT PROJECT

## PURPOSE

Initialize the project baseline with a minimal, clean Three.js + TypeScript setup.

This directive establishes the technical starting point for all future development.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md
- docs/foundation/tech-stack.md

Load the following skill references:

- docs/skills/context7.md

---

## GOAL

Create a working application scaffold that:

- runs in the browser
- renders a blank scene using Three.js
- uses TypeScript in a pragmatic, minimal way
- has a deterministic update loop

No gameplay logic is implemented in this directive.

---

## CONSTRAINTS

- Use TypeScript without advanced type features
- Do NOT introduce gameplay systems
- Do NOT introduce ECS or external game frameworks
- Do NOT allocate objects inside the update loop
- Keep the setup minimal and readable

---

## FILES TO CREATE

Create the following files:

```
src/
├─ main.ts
├─ core/
│  ├─ Game.ts
│  ├─ Engine.ts
│  └─ Time.ts
├─ renderer/
│  ├─ Renderer.ts
│  ├─ Scene.ts
│  └─ Camera.ts
```

Project config files (vite, tsconfig) may be added if required.

---

## IMPLEMENTATION STEPS

1. Initialize a Vite + TypeScript project
2. Install Three.js as the rendering dependency
3. Create a single HTML entry point
4. Implement a basic render loop
5. Separate rendering, timing, and engine control
6. Render an empty scene with a solid background color

---

## UPDATE LOOP REQUIREMENTS

- Single global loop
- Uses requestAnimationFrame
- Delta time calculated via Time utility
- No allocations inside the loop

---

## RENDERING REQUIREMENTS

- Orthographic camera
- Fixed viewport
- No postprocessing yet
- No scene graph mutations per frame

---

## VALIDATION CHECKLIST

This directive is complete when:

- The project builds successfully
- A blank scene renders in the browser
- The update loop runs consistently
- No gameplay systems exist yet
- The codebase matches the defined folder structure

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Input handling
- Gameplay systems
- Asset loading
- UI
- Effects

---

## FINAL NOTE

This directive establishes the foundation for all subsequent directives.

If any step introduces unnecessary complexity, it must be simplified.
