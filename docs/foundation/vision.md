# PROJECT VISION (AI FOUNDATION)

## PURPOSE OF THIS DOCUMENT

This document defines the immutable vision of the game project.
It is used as **foundational context for AI agents** executing directives.

This file:

- MUST be treated as read-only by AI agents
- MUST NOT be modified during implementation
- MUST be loaded as context for all gameplay-related directives

---

## GAME OVERVIEW

The project is a **single-player top-down space shooter** inspired by classic arcade shooters, reimagined as a **modern, readable bullet hell** with strong visual feedback and controlled complexity.

The game focuses on:

- deterministic enemy waves
- readable projectile patterns
- player skill and positioning
- visual clarity over chaos

The game is NOT a simulation.
The game IS a scripted, data-driven combat experience.

---

## CORE GAMEPLAY LOOP

1. Player selects a map
2. Player enters a combat stage
3. Enemies appear in scripted waves from the top of the screen
4. Player destroys enemies while dodging projectile patterns
5. Enemies drop:

   - coins (meta-progression)
   - temporary power-ups (run-only)

6. After completing all waves, a boss may appear
7. Player wins or loses
8. On loss: full run reset
9. On win: unlock next map and/or progression

---

## PLAYER EXPERIENCE GOALS

The player should feel:

- full control over movement
- responsibility for mistakes
- fairness in difficulty
- satisfaction from learning patterns
- visual feedback for every important action

The game rewards:

- positioning
- pattern recognition
- calm movement

The game does NOT reward:

- random reactions
- memorization without understanding
- passive play

---

## DESIGN PHILOSOPHY

- The game is **pattern-driven**, not AI-driven
- Enemies are actors following scripts, not decision-makers
- Projectiles are the primary language of danger
- Visual effects enhance feedback but never affect logic
- All gameplay-relevant behavior must be deterministic

---

## PROGRESSION MODEL

Two separate progression layers exist:

### 1. Meta Progression (Between Runs)

- Uses coins
- Unlocks or upgrades base player stats
- Persists between runs

### 2. Run Progression (Within a Run)

- Uses temporary power-ups
- Affects weapon patterns, shields, or health
- Fully resets on death

These two layers MUST remain strictly separated.

---

## NON-GOALS (IMPORTANT)

The project explicitly does NOT aim to:

- be a roguelike or full roguelite
- use procedural or random wave generation
- feature emergent AI behavior
- simulate physics-heavy interactions
- support multiplayer

Any system or implementation that moves toward these goals is considered incorrect.

---

## IMMUTABLE CONSTRAINTS

The following constraints MUST be respected by all systems and directives:

- All gameplay systems must be data-driven
- Logic and visuals must be strictly separated
- No system may directly control another system
- Systems communicate only via shared data or events
- Performance stability is prioritized over visual excess

---

## TARGET PLATFORM

- Desktop-first
- Mouse and keyboard primary input
- Mobile support considered via input abstraction

---

## FINAL NOTE

If a design or implementation decision conflicts with this document,
this document takes priority.

Any ambiguity should be resolved by choosing the option that:

- reduces complexity
- improves readability
- preserves determinism
