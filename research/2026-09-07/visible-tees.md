# Visible tees / S3 research

**Status:** read-only source review, 2026-09-07. The Mermaid checkpoint remains **written, unrun, and unrendered**; this report makes no visual, parity, or real-image claim.

## Source-grounded result

Remote heads inspected: `lab/stages-s3` at `ac369f1e4584083d121e72211f5530a287b10da4`; `lab/dashs-ternary-edge-pattern` at `b9d05cdd26b352641f582c53a52d1ae2712d8271`; `continuation/intake-engine` at `7fbd6b9225b8d182f2569cffc5cf09d3f0c0ebdf`. GitHub commit search returned no G3/S3-named commits, so the branch heads and fetched source are the history evidence, rather than an inferred commit series.

### The historical G3 implementation

`continuation/intake-engine:packages/alg/src/detectors/threeFactor/features/g3.teeFamily.ts` (head `7fbd6b9`, blob `f68e3a7`) is a legacy **EngineUnit refinement**, not a new object stage:

- It consumes `stage`, `tees`, and `viewport`, and produces `tees` again. It examines only `TeeEvidence.tier === 'ring'`; `component` and `recovered` tees pass through unchanged.
- Each ring is paired with the smallest eligible enclosing bright component. The winning anchor-family compares **major, minor, area, and fill** by log-ratio. Frames are stage-local while legacy tees are original-image coordinates, so the frame gets the Y-only `+viewport.topPx` adjustment before containment.
- The output filters the original `tees` sequence, retaining `detId` and order. It supplies accepted, rejected, and informational overlay drawables plus values/reasons. It does not establish a hole assignment or alter straight-test angle semantics.
- Its own historic research record (`docs/unported/g3-intact-tee-family.md`, esp. §§3–4) says the source had only synthetic tests and no committed real-image evidence; a count check belonged to the **G3 gate**, not the selector. This must not be recast as a past validation result.

The Dashs ternary branch head is `b9d05cdd`, and contains the surrounding Dashs evidence/resume work. It should be treated as a compatible legacy consumer of the `tees` slot, not evidence that S3 Parts have the legacy field shape.

### S3 implementation and Parts

`lab/stages-s3:packages/alg/src/stages/S3/clean/Tee.ts` (head `ac369f1`, blob `8eef2eb`) defines a fresh, explicit Part sequence:

| Tick / Calculation | Consumes | Produces | Meaning |
|---|---|---|---|
| `Tee.detectRings` / `fn.Tee.detectRings` | `px.components`, `px.badges` | `px.tees.rings` | finds enclosed bright holes, keeps `tee-rect`, rejects centers covered by `Badge.has.mute.px` |
| `Tee.findFamily` / `fn.Tee.findFamily` | `px.tees.rings`, `px.components` | `px.tees.family` | pairs each candidate with an enclosing bright component and picks a major/minor/area anchor-family |
| `Tee.findPx` / `fn.Tee.findPx` | `px.tees.family`, `px.components` | `px.tees` | calls once per accepted member and materializes that exact bright component's raster pixels |

`lab/stages-s3:.../clean/index.ts` (blob `f9f449d`) declares the three ordered S3 ticks, binds the named functions, executes through `executeCompiledPlan`, and composes PCR from returned testimony. It requires both prior Parts before execution. `packages/alg/src/stages/S3/contract.ts` produces seven receipt/panel steps and says recovery and component fallback are `NOT RUN`; `materializeS3Subtraction` returns a derived alpha-raster only and does not mutate PxC.

**Compatibility decision:** this is partly a shape conversion and partly an algorithm choice. A bridge can create a legacy-looking visible-tees projection from S3 objects (`detId` must be stable at the bridge, center/bbox/angle/visible pixels/provenance), but cannot truthfully claim equivalence without choosing what to do about these behavior differences:

1. G3 uses a stage-local-to-original-image Y alignment; S3 expects common cropped coordinates (`topPx: 0`).
2. G3 family membership includes fill; clean S3 deliberately uses only major/minor/area. S3 has a separately gated `exp/fill-consistent` variant, which proves the difference is intentional.
3. G3 refines mixed `ring/component/recovered` candidates and emits per-rejection evidence; clean S3 emits only visible ring-derived `Tee` objects and has no recovery/fallback output.
4. G3 uses bbox geometry for presentation but S3 `Tee.px` is exact accepted-component ownership. A bbox must never be converted to owned pixels.

Therefore no re-recognition is needed for wiring, but the addresses must be bridged deliberately: S3 consumes legacy `BadgePxC.objects.address`, `px.badges`, plus `px.components`; the new Mermaid S1 declaration publishes `px.badges.objects`. Existing components satisfy the other S3 prerequisite. Conversion is needed only where a legacy `TeeEvidence[]` consumer remains, and it must name lost/reinterpreted fields and preserve source identity.

## Mermaid proof versus the required infrastructure

At review head `b5a6ae040147b488bc44ea94c6303296b2ecde78`, `experiments/mermaid-s0-s1/HANDOFF.md` explicitly says **unrun/unrendered** and calls the interpreter isolated with no shared executor, Stage routing, browser inspection, or S2 compatibility. `runner.ts` also labels it “not yet the shared PQL executor.”

| Requirement | Prototype status | Evidence / smallest consequence |
|---|---|---|
| Direct `fn` result reuse | implemented in source; unrun | `values: Map` resolves `binding.kind === 'fn'`; results never become PxC Parts unless `into` is present. |
| Named composite-child tracing | missing | runner only writes one `CallRecord` per authored YAML calculation; `PxC.call` inside a registered calculation is invisible. S3 `Tee.findPx` is exactly this per-member child-call case. |
| Collection/per-object calls | missing shared child testimony | S3 already maps internally over family members. Ordinary map plus a shared named-call API can expose a stable child key and per-item testimony; authored `forEach` syntax is optional convenience, not a demonstrated need. |
| Branches, rejections, empties | function-level flow is sufficient; unrun | an ordinary calculation can branch and return rejected/empty values, which can flow by direct result. The graph has no conditional syntax or required outcome/receipt shape, but that does not block composite calculation branching. |
| Stage input/output contract | missing | compiler checks graph ordering and publication only; it does not require a declared Stage input/output Part contract or compare it with actual PxC traffic. |
| Failure prefix | partial | `MermaidExecutionError` retains the successful prefix in `run.calls` and marks the failed call, but no stable run/source identity is attached. |
| Source/run identity | missing | run record has only PCR name/calls; it does not identify source bytes, calc/dependency identity, Run Args, upstream Part identities, or materialization identity. |

The existing shared executor is reusable: `exec/gateway.ts` already serializes Ticks, freezes declared calculation identities, and checks tracked `get`/`set` reads/writes. Its current blind spot is calculation invocation (`register`, `call`, and nested calls are not tracked), so a declared `fn.*` may be bound without proving it ran.

## Bounded implementation tasks

| Task | Owns / depends on | Acceptance demonstration | Smallest falsifier |
|---|---|---|---|
| **1. Trace calculation invocation at the shared PxC call boundary** | `exec/board.ts`, `exec/gateway.ts`; uses existing Tick testimony | an S3 run shows each Tick and the exact `fn.*` calls, including one `findPx` call per accepted member, in order; failure contains preceding calls | register/bind `fn.Tee.findPx` but do not invoke it: testimony must not report it as called |
| **2. Promote the small composition runner into the gateway as an adapter, with direct-result bindings and Stage I/O declaration** | depends on 1; owns Mermaid adapter/compiler output and a narrow S3 composition contract | compile/run a three-Tick S3 declaration against existing `px.components`/`px.badges`; declaration and actual Part traffic agree; emitted PCR is made from shared testimony | omit `px.badges` or add an undeclared read/write: run fails before a PCR is presented |
| **3. Record keyed child calls and outcome records through ordinary map** | depends on 1–2; owns the shared named-call API/instrumentation | `Tee.findPx` materializes N keyed child calls for N family members; an empty family yields an explicit empty outcome, not “never ran” | reorder members or throw on member 2: identity/order and successful prefix must expose the change |
| **4. Project existing S3 results for legacy consumers, only where needed** | depends on 2; owns one explicit adapter at legacy `tees` seam | a receipt shows source Part identities plus projected legacy fields; exact S3 `px` remains ownership and bbox remains geometry | a consumer receives a bbox-derived pixel set or a changed `detId`: adapter rejects/flags it |

Tasks 1–2 are necessary now for Luna-authored calculations to acquire shared wiring, execution, and inspection. Task 3 is necessary when S3 needs readable per-object calculation testimony; declarative `forEach` may be added later only if ordinary map becomes inadequate for readable authoring. Task 4 is only needed if the Dashs/legacy EngineUnit path must consume S3 results. General scheduling, a full PQL grammar/schema, compiler optimization, and re-recognition are later work with no concrete code need from this evidence.
