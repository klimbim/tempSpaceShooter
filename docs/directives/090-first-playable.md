# DIRECTIVE 090 — FIRST PLAYABLE

## PURPOSE

Assemble all implemented systems into a complete, playable game loop.

This directive finalizes the MVP by enabling damage, death, basic HUD,
and a full run lifecycle from start to restart.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/player-system.context.md
- docs/systems/enemy-system.context.md
- docs/systems/boss-system.context.md
- docs/systems/collision-system.context.md
- docs/systems/drop-system.context.md
- docs/systems/wave-system.context.md

Load the following skill references:

- docs/skills/context7.md
- docs/skills/data-driven-design.md

---

## GOAL

Create a fully playable MVP that:

- starts a run
- spawns waves and enemies
- allows the player to move and shoot
- applies damage via collision events
- ends the run on player death
- allows restarting the game

---

## CONSTRAINTS

- Do NOT introduce new systems
- Do NOT add advanced UI or menus
- Do NOT add sound or postprocessing
- Keep logic explicit and readable
- Preserve deterministic behavior

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/core/
├─ Game.ts

src/ui/
├─ HUD.ts
```

Existing systems are wired together; no refactors.

---

## DAMAGE ENABLEMENT

Wire collision hit events to damage handling:

- Player System:

  - consumes hit events
  - reduces shield or HP

- Enemy and Boss Systems:

  - consume hit events
  - reduce HP

Damage values are taken directly from projectile data.

---

## DEATH HANDLING

Define explicit death conditions:

- Player death when HP reaches zero
- Enemy death when HP reaches zero

On player death:

- stop wave progression
- clear active entities
- show restart option

---

## RUN FLOW

Implement the minimal run lifecycle:

1. Game start
2. Initialize player and systems
3. Start wave sequence
4. Run until player death or final wave cleared
5. Show end state
6. Restart resets run-based state

Meta progression is stubbed.

---

## BASIC HUD

Implement a minimal HUD displaying:

- player HP
- player shield
- coin count

HUD reads state only; no logic.

---

## VALIDATION CHECKLIST

This directive is complete when:

- The game can be played from start to death
- Player and enemies can damage each other
- Drops are collected and applied
- HUD reflects current state
- Restart works reliably

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Sound and music
- Advanced UI
- Boss-specific encounters (optional)
- Postprocessing effects

---

## FINAL NOTE

This directive defines the first complete playable version.

Any feature not required to play the game must be postponed.
