# Graphics Logic

This document defines **how graphics work** in the project.
It exists to prevent AI agents from misusing visuals as logic.

Graphics are **data-driven visualization**, not gameplay.

---

## Core Rule

> Graphics reflect game state.  
> Graphics never define, influence, or decide gameplay.

If a behavior exists only in graphics, it does not exist in the game.

---

## One-Way Flow

Game State → Visual State → Renderer

- Game State is authoritative
- Visual State is derived
- Renderer is passive

There is **no reverse flow**.

---

## Asset Types

All graphic assets live under `assets/` and are strictly categorized.

### 1. Sprites

Sprites represent entities:

- player
- enemies
- bosses
- projectiles
- drops

Sprites are **2D textures rendered on planes**.

Sprites are:

- square-based
- centered
- visually aligned with logical position

---

## Sprite Dimensions (Canonical)

Sprite height defines its **visual scale class**.

These values are fixed and must not be altered by AI agents.

| Category    | Height (px) |
| ----------- | ----------- |
| Boss        | 128         |
| Enemy       | 64          |
| Player      | 64          |
| Coin        | 16          |
| Power-up    | 48          |
| Projectiles | Variable    |

Width may vary only due to animation sequencing (see below).

---

## Sprite Sequencing (`*-sec`)

Any sprite file ending with `-sec` is a **sequence sprite**.

### Rules for sequence sprites

- Frames are laid out **horizontally**
- Each frame is a **square**
- Frame size = image height
- Number of frames = image width / image height

Example:

- Image size: `512 x 64`
- Frame size: `64 x 64`
- Frames: `512 / 64 = 8`

Sequence sprites:

- must not encode logic
- must not affect gameplay timing
- are driven by Visual State only

---

## Animation Rules

Animations:

- are time-based
- read Visual State
- never trigger gameplay events

Allowed:

- explosions
- engine flicker
- shield pulse
- weapon glow

Forbidden:

- animation completion triggering damage
- animation state controlling logic
- animation-driven collisions

---

## Visual State

Visual State is derived from Game State and may include:

- frame index
- animation progress
- glow intensity
- shield opacity
- engine thrust intensity
- destruction progress

Visual State:

- can be rebuilt at any time
- may interpolate values
- may drop detail for performance
- must never be read by gameplay systems

---

## Renderer Responsibilities

Renderer:

- reads Visual State
- updates meshes, UVs, materials, shaders
- applies camera effects
- applies post-processing

Renderer must not:

- update timers
- change Game State
- detect collisions
- trigger events

---

## Shaders

Shaders:

- are stateless
- receive uniforms only
- are replaceable

Shaders must not:

- track time independently of Visual State
- encode gameplay rules
- affect hit detection or logic

---

## Camera

Camera is visual-only.

Camera may:

- shake
- move for intro / outro
- add cinematic effects

Camera must not:

- affect gameplay timing
- affect collisions
- affect positions in logic space

---

## Backgrounds

Background assets are organized as:

- `backgrounds/layers` — static or scrolling layers
- `backgrounds/objects` — decorative elements
- `backgrounds/tiles` — repeating textures

Backgrounds:

- have no gameplay meaning
- are never queried by logic
- do not affect collisions or movement

---

## Performance Rules

- Visual degradation is allowed
- Logic degradation is forbidden
- Animation skipping is allowed
- Determinism must be preserved

---

## Summary

Graphics are a **view**.
Game systems are the **model**.

Never mix them.
