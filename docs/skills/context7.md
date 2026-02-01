# SKILL — CONTEXT7

## INTENT

Enforce strict minimal-context reasoning.

This skill assumes that an external Context7-like mechanism may limit or prune context.
The agent must behave correctly even when only partial information is available.

---

## RULES

- Use **only** documents explicitly loaded in the current directive
- Do NOT rely on memory from previous directives or conversations
- Do NOT assume missing context exists
- Do NOT infer hidden architectural decisions
- Prefer local reasoning over global assumptions

---

## OPERATING MODE

- Treat each directive as an isolated task
- If required information is missing, ask or fail explicitly
- Follow written contracts over inferred intent

---

## GOAL

Reduce hallucinations, prevent context leakage, and minimize token usage.

If context is insufficient, correctness is preferred over completeness.
