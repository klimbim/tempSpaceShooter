# SKILL — WEBGL PERFORMANCE

## INTENT

Bias all rendering- and simulation-adjacent decisions toward predictable, high performance.

This skill enforces a GPU-first mindset and prevents common performance traps
in WebGL / Three.js–based games.

---

## CORE PRINCIPLES

- Avoid per-frame allocations
- Batch work whenever possible
- Prefer stable memory usage over flexibility
- CPU prepares data, GPU does the heavy lifting

Performance is a design constraint, not a post-optimization step.

---

## PREFERRED PATTERNS

- Object pooling for frequently created entities
- Reuse vectors, matrices, and buffers
- Fixed-size arrays or pools over dynamic collections
- Simple math over complex abstractions

Measure first, then optimize deliberately.

---

## AVOID

- Allocating objects inside update loops
- Creating or destroying Three.js objects per frame
- Frequent scene graph mutations
- Deep object hierarchies
- Excessive state changes per draw call

If something allocates every frame, it is wrong.

---

## DECISION RULES

When faced with a trade-off:

- Prefer fewer draw calls over cleaner abstractions
- Prefer reuse over recreation
- Prefer explicit control over convenience APIs

If performance cost is unclear, assume it is too high.

---

## WHEN TO USE

- Projectile-heavy systems
- Collision and hit detection
- Visual effects with many instances
- Any logic running every frame

Avoid using this skill for tooling or one-off setup code.

---

## GOAL

Maintain stable frame times and predictable performance
under peak load conditions.

Consistency is more important than peak visual quality.
