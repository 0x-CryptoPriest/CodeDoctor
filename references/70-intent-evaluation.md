# Intent Evaluation

Use this file on every review and every repair pass.

## Build the intent map
Build two layers of intent.

### Request intent
Start from high-level project anchors:
- README / docs
- ADRs / design notes
- task or issue docs
- tests and fixtures
- public API / routes / CLI
- config files

### Project role intent
Infer what the touched code means inside the project:
- Which module, route, command, component, worker, adapter, or test surface owns this behavior?
- Who calls it, what does it call, and what ordering or invariants do callers depend on?
- What data enters, changes shape, persists, leaves the system, or crosses trust boundaries?
- Which user workflow, public contract, background job, integration, or admin operation does it support?
- Which tests or fixtures describe expected behavior, and which important behavior is only implicit in callers?

Keep it lightweight. Do not sweep the whole repo unless the anchors are weak, contradictory, or the code role is unclear.

## Intent block
Before findings, write a short intent block:
- Goal
- Non-goals
- Constraints
- Success criteria

The block should reflect both the user's immediate request and the inferred project role of the touched code.

## Review rule
Judge code against both:
1. The explicit request intent
2. The inferred project role intent
3. The technical correctness and quality gates

If implementation is technically correct but misses intent, mark it as `Intent Miss`.

## Priority order
1. Task / issue / PR description
2. Repo docs / ADRs / README
3. Tests / fixtures
4. Existing public behavior
5. Nearby code
6. Structural inference from callers, callees, data flow, and runtime entry points

If these conflict, follow the order above.

## Ambiguity rule
- Infer conservatively.
- Mark unresolved ambiguity as `Intent Risk`.
- Ask only when the ambiguity changes behavior, scope, data migration, authorization, or API contract.

## Hard blocker
`Intent Miss` is a blocker even if the code compiles and tests pass.

## Repair loop
Rebuild the intent map on every repair pass.
Re-check the changed code against the new intent before deciding that the work is done.
