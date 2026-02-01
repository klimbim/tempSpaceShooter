# DIRECTIVE 040 — WAVE SYSTEM

## PURPOSE

Implement the Wave System as a deterministic, data-driven scenario controller.

This directive introduces real combat structure by orchestrating enemy waves
without embedding enemy or gameplay logic.

---

## CONTEXT TO LOAD

Load the following documents as read-only context:

- docs/foundation/vision.md
- docs/foundation/principles.md
- docs/foundation/constraints.md

Load the following system contexts:

- docs/systems/wave-system.context.md
- docs/systems/movement-patterns.context.md
- docs/systems/enemy-system.context.md

Load the following skill references:

- docs/skills/context7.md
- docs/skills/data-driven-design.md
- docs/skills/deterministic-systems.md
- docs/skills/bullet-hell-design.md

---

## GOAL

Create a Wave System that:

- sequences waves deterministically
- spawns enemies via explicit data definitions
- controls wave start/end conditions
- integrates cleanly with the core loop

No player input or combat resolution is implemented yet.

---

## CONSTRAINTS

- Do NOT implement enemy logic
- Do NOT implement shooting or damage
- Do NOT introduce randomness
- Do NOT allocate memory during update loops
- Waves must be fully data-driven

---

## FILES TO CREATE OR UPDATE

Create or update the following files:

```
src/systems/
├─ WaveSystem.ts

src/data/
├─ waves/
│  ├─ wave-set-01.ts
```

Wave data files may be simple TypeScript exports.

---

## WAVE DATA MODEL

Define a wave data structure that includes:

- waveId
- entryDelay
- spawnGroups
- endCondition
- rewardPolicy (placeholder)

The data model MUST match the wave system context.

---

## SPAWN GROUP MODEL

Each spawn group must define:

- enemyType
- count
- spawnInterval
- spawnPattern (position logic)
- movementPattern
- shootPattern (placeholder)

Spawn groups are declarative and non-reactive.

---

## WAVE FLOW IMPLEMENTATION

Implement explicit wave state handling:

1. Idle
2. Waiting (entry delay)
3. Spawning
4. Active
5. Completed

Transitions MUST be explicit and deterministic.

---

## ENEMY SPAWN INTEGRATION

- Wave System requests enemy spawns from Enemy System
- Full enemy configuration is passed at spawn time
- Wave System does not track enemy behavior

Enemy System owns enemy lifecycle after spawn.

---

## END CONDITIONS

Implement deterministic end condition evaluation:

- all enemies defeated
- fixed duration expired
- required enemies defeated

End conditions must be declared in data.

---

## UPDATE LOGIC

Per update tick:

- Update wave timers
- Trigger spawn groups at defined times
- Evaluate end condition
- Advance wave state if conditions are met

No per-frame scanning of global enemy lists.

---

## VALIDATION CHECKLIST

This directive is complete when:

- Waves progress in a fixed order
- Enemies spawn according to wave data
- Entry delays and spawn intervals work correctly
- Wave completion is deterministic
- No gameplay logic exists in Wave System

---

## OUT OF SCOPE

Explicitly excluded from this directive:

- Player interaction
- Enemy AI or shooting
- Boss encounters
- Drop spawning

---

## FINAL NOTE

The Wave System defines the rhythm of the game.

If wave logic becomes reactive, implicit, or state-heavy,
it must be simplified.
