# Sprite Contract

This document defines what a sprite asset is and how it must be interpreted.

Sprites are **dumb visual data**.
They do not encode behavior, logic, or state.

---

## Sprite Definition

A sprite is a 2D texture rendered on a plane.

Sprites:

- are square-based
- are centered
- do not define hitboxes
- do not define gameplay meaning

---

## Naming Conventions

- `*-sec.png` — sequence sprite (animated)
- all other sprites are static

No other suffixes are allowed.

---

## Sequence Sprites (`*-sec`)

Sequence sprites represent **visual animation only**.

Rules:

- frames are laid out horizontally
- each frame is a square
- frame size = image height
- frame count = image width / image height

Sequence sprites:

- must not encode timing logic
- must not encode phases
- must not encode damage states

---

## Canonical Sprite Sizes

Sprite height defines its **visual scale class**.

These sizes are fixed.

| Category    | Height (px) |
| ----------- | ----------- |
| Boss        | 128         |
| Enemy       | 64          |
| Player      | 64          |
| Coin        | 16          |
| Power-up    | 48          |
| Projectiles | Variable    |

Width may only vary due to sequencing.

---

## Transparency and Alignment

- transparent background required
- visual center must align with logical position
- no baked-in offsets

---

## Forbidden Practices

Sprites must not:

- encode hitboxes
- encode phases
- encode damage or HP
- encode timing assumptions
- require special-case code

If a sprite requires logic to be interpreted correctly, it violates this contract.
