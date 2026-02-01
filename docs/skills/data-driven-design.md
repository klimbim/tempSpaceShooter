# SKILL — DATA-DRIVEN DESIGN

## INTENT

Enforce data-first architecture and eliminate logic-driven behavior.

This skill biases the agent toward designing systems as executors of data,
not decision-makers.

---

## CORE PRINCIPLES

- Data defines behavior, code executes it
- Configuration over conditionals
- Composition over inheritance
- Explicit structures over implicit logic

If behavior cannot be expressed as data, it is likely incorrect.

---

## PREFERRED PATTERNS

- Plain data objects for configuration
- Declarative definitions (waves, enemies, patterns)
- Explicit state machines
- Small, predictable update steps

Behavior changes should require data changes, not code changes.

---

## AVOID

- Hard-coded behavior
- Deep if/else trees
- Hidden defaults
- Implicit state transitions
- Logic that depends on external system state

---

## DECISION RULES

When choosing between approaches:

- Prefer static data over dynamic logic
- Prefer tables over branching
- Prefer explicit parameters over inferred behavior

If logic grows, extract it into data.

---

## WHEN TO USE

- Gameplay systems
- Wave, enemy, boss definitions
- Movement and shooting patterns

Do not use for low-level utilities or rendering setup.

---

## GOAL

Reduce complexity, increase predictability, and enable safe AI-assisted development.

Correctness and clarity are more important than flexibility.
