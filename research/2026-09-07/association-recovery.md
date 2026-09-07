# S4 / historical G4 association and recovery — research ledger

**Scope.** Read-only recovery of the tee/basket association record and constrained tee recovery, for authors of Calculations and a readable graph/YAML. The local target is based on `fa44a4505d9aafbf6d2d21a12400298edb7fa96d`; the separately published, **unrun** S0/S1 Mermaid review checkpoint is `b5a6ae040147b488bc44ea94c6303296b2ecde78` on `review/s0-s1-mermaid-b5a6ae0` (2026-09-07). No fresh run was requested or performed.

## Evidence classification

| Class | What was inspected | What it establishes |
|---|---|---|
| Source inspected | `b9d05cdd26b352641f582c53a52d1ae2712d8271`: `packages/alg/src/detectors/threeFactor/features/g3.teeRecovery.ts`, `g4.teeBadgeLock.ts`, `g4.teeBadgeLockMath.ts`, `g4.teeBadgeLockReceipt.ts`, `assignment.ts`, `occlusion.ts`, and the Claims Ledger/Ratchets. | Historical algorithm shape and its explicit failure vocabulary. File names are historical; use each feature's declared `gate`, not its filename. `teeRecoveryFeature.gate` is `G4`; `g4SearchFeature.gate` is `G6`; do not conflate either with an S-stage. |
| Source inspected | `43829313870fc0b792782e5ce751b924de07f684` (2026-09-06), “Checkpoint S1 YAML composition, calculation variants, and JS inspection”; current S1 assembly/ownership sources at `fa44a45`. | Existing named-PQL/YAML precedent and that alternatives/incomplete material can be ordinary calculation output. |
| Source inspected, **unrun** | `b5a6ae0`: `experiments/mermaid-s0-s1/{S0,S1}.mmd`, `packages/alg/src/stages/S0/exp/mermaid-pcr/{compiler,runner,README,REFINE}.ts/md`. | A deliberately bounded experimental compiler/interpreter. It claims no parity, rendering, shared PQL, normal stage routing, browser inspection, or S2 compatibility. |
| Saved run evidence | `docs/CLAIMS-LEDGER.md` rows 1–5, 8, 10–12; `docs/RATCHETS.md`. | These documents cite prior artifacts and receipts, but their files were not present in this checkout. Their historical claims are recorded evidence, not a new reproduced result. The Ratchets explicitly mark recovery axis/claim-distance values **not yet pixel-verified**. |
| Unverified here | Current corpus acceptance, exact legacy commit resolution for abbreviated `dc96000` / `ae68617`, and all artifact-file contents mentioned in the ledger. | Do not promote these to current proof without the cited artifact plus pixel receipt. |

## Historical contract: recovery is constrained evidence, association is a separate decision

`g3.teeRecovery.ts` declares a `TeeRecoveryCandidate` with a course-local `RecoveryFit`, all `fragmentPixels`, component IDs, badge ray/axis, `consideredComponentsGlobal`, and `ambiguityLostToBadgeLabel`. `graphCandidateResult` yields a `TeeRecoveryResult` with `accepted|rejected`, a named reason, values, and oriented corners. A successful `teeRecoveryUnit` publishes a `RecoveredTeeInput` with provenance source `tee-shard-recovery`; a rejection remains overlay/measurement evidence.

Its recovery procedure is meaningful evidence, not a blind fill:

1. Start with *unassigned numbered badges* and the whole canonical bright-component set.
2. Subtract known owned pixels and opaque/basket/screen-chrome pixels at pixel granularity; preserve a component's remaining remnant. This follows the stated z-order rule: a basket may merge with a tee, and neither a component nor a basket bbox may be dropped whole.
3. For each target badge, fit the course-measured hollow tee support against every visible candidate component/group. The fit requires at least eight support pixels, no unexplained visible pixels, and a badge-ray axis within the active tolerance. It uses course-local pad medians and support thickness; it does not invent a fixed tee template.
4. Retain a deterministic winner **and runner-up alternatives** per target. Cross-target reuse of the same component set becomes a named rejection for the loser (`ambiguityLostToBadgeLabel`), selected by lower axis error, never loop order.
5. Dedupe an accepted recovery against existing/recovered tees, then rerun global assignment only when additions exist.

The historical correction matters: predecessor-basket spatial discovery was a false worldview. Claims Ledger row 3 upholds replacing it with predicate-as-filter over all unowned bright components. Ledger rows 1–2 retract apparent recovery evidence that was actually badge digits. The status vocabulary therefore needs at least:

| State | Meaning required by the record |
|---|---|
| `observed` | Pixels/geometry exist in an immutable source and have an identity. |
| `partial` | A visible remnant or a basket path trace exists but is incomplete; retain it with the source and reason. |
| `inferred` | A constrained fit or selected association is derived from observed evidence; it must name inputs, predicate and alternatives. |
| `unknown` | Identity, basket endpoint, or viable candidate is unresolved; it is a successful diagnostic result, never a silent absence. |
| `rejected` | A specific considered candidate fails a named predicate, or loses an explicit ambiguity/duplicate decision. |

`g4.teeBadgeLock.ts` is a distinct, opt-in association operation (`teeBadgeLockFeature`, default OFF). It takes `assignment.scoredPairs`/raw pair evidence plus tees and badge evidence; `collapseTeeBadgePaths`, `scoreTeeBadgeCandidates`, and `maximumWeightOneToOne` form tee↔badge locks. `traceBasketsForLocks` then follows each accepted tee–badge path and records either a basket endpoint or an `unknown` partial trace. The receipt wording already preserves that distinction: a traced path with no endpoint is “UNKNOWN basket, partial trace kept as evidence.” Association does **not** prove a recovery and recovery does **not** prove a basket association.

Basket treatment is constrained by the CV engram: basket ownership follows sprite/border ink, not a bbox, because an occluded tee pad can leave a remnant in the empty margin. Badge ownership is different: owning all pixels in the badge outer-border bbox is intentional. Current S1 provides this exact precedent: `declare`, `owned`, `muted`, and `remaining` in `stages/S1/exp/badge-assembly/ownership.ts` preserve explained component pixels separately from `unaccountedButOwned` bbox pixels.

## What the current Mermaid prototype composes—and what it cannot record

The b5a6ae0 graph already makes inputs, outputs, tick grouping, and the S1 relation alternatives readable. `findRelated` returns all matches; `assemble` preserves every border alternative and returns `incomplete` rows with reasons. This is the correct model for recovery/association alternatives: publish one immutable result object with its candidates/alternatives/rejections rather than allow competing writers to one PxC address.

`compileMermaidPcr` supports a small declaration-ordered graph: named fn/PxC bindings, direct function-result arrows, a single publication per calculation, and one writer per PxC address. `executeMermaidYaml` can already pass arbitrary ordinary values: relation alternatives, confidence/state records, and a composite function's complete evidence object can flow through a binding. Explicit `into` outputs are written to PxC. Direct function intermediates and the `RunRecord` itself remain in the in-memory value map/returned record rather than a run-record PxC address. `CallRecord` contains tick, calculation ID, bindings, resolved inputs, output, status and error. The gap is not value flow or a dedicated relation/state syntax. It is durable occurrence identity, parent/child nesting, lightweight immutable source-reference/version discipline, and inspector support for these values as evidence. Its own README says it is not the shared executor.

### Keep inside ordinary named composite functions

These are algorithm-internal loops. They need a clear output type and per-item evidence, but not graph-language control flow:

- pixel subtraction, 8-connected shard splitting, center/angle scanning, support residual ranking, two refit passes, dedupe, and recovery winner selection inside a `recoverTeeEvidence` calculation;
- candidate-collapse/scoring and `maximumWeightOneToOne` inside an `associateTeeBadge` calculation;
- the association optimizer's exchange passes (`assignment.ts` / `g4.search.ts`); and
- S1-style relation filtering/assembly when its output carries all alternatives and `incomplete` reasons.

A calculation result should expose `observedSources`, `candidateAlternatives`, `selected`, `rejected`, and `unknown/partial` outcomes. This keeps authored graphs legible and avoids speculative scheduler/cache/schema work.

### Genuinely needed composition semantics

The required execution capability is **keyed nested named invocation testimony**, callable from an ordinary composite function's existing loop. The relevant case is: for every accepted tee↔badge lock, the composite invokes named `traceBasket` and preserves one child occurrence per lock. A generic internal JS loop cannot honestly advertise those as named graph calculations today.

The shared child-invocation mechanism needs a stable item key, child calculation occurrence ID, parent occurrence ID, per-child bindings/source references, child status/result/error, and partial-prefix retention. It must support a child result of `unknown`/`partial` without converting it to execution failure. This is a tracing requirement; it does not require a broad scheduler or unrestricted control-flow language. YAML `forEach`/map syntax is only an optional convenience, to be added after a pilot demonstrates authors need it rather than calling the child mechanism from an ordinary composite function.

## Bounded infrastructure tasks for the next implementation pass

| Task and owner files | Depends on | Demonstration | Falsifier |
|---|---|---|---|
| **1. Execution occurrences with stable source references.** Owner: executor seam (`packages/alg/src/exec/` or successor), with the Mermaid runner only as a migration fixture. Give every calculation invocation an occurrence ID, status, binding-to-source record, output publication/provenance, and a lightweight immutable source-reference/version. Do not deep-copy raster values. | Existing `CallRecord` shape and explicit PxC publications. | Two named calculations consume the same raster; receipt shows their distinct occurrence IDs and the exact source occurrence/address/version. | Rebinding or later writing an address makes an earlier record’s source ambiguous. |
| **2. Keyed nested named child invocation.** Owner: execution seam plus a focused fixture; child function remains owned by its algorithm module. Let an ordinary composite function invoke named `traceBasket` for each existing-loop item, yielding child occurrences under a parent. Consider graph/YAML `forEach` only after a pilot proves authors need syntactic convenience. | Task 1. | Three accepted locks invoke named `traceBasket`; receipt shows three child IDs keyed by lock, two basket endpoints and one `unknown` partial trace. | A child is untraceable, child key is unstable, or one partial/failed child erases already completed sibling records. |
| **3. Constrained recovery evidence composite.** Owner: a new recovery calculation module and its graph/YAML sample; do not alter historical detector code during the first pass. Return observed immutable sources, candidate alternatives, all rejections, selected fit, ambiguity/duplicate decision, and a `recovered|unknown|rejected` outcome. | Task 1 for source links; no task 2 required. | Fixture with badge overlap, basket overlap, and a global far component prints all considered components and names the winner/rejection. | A component disappears without an identity/reason, bbox subtraction erases a tee remnant, or a recovery is accepted with unexplained pixels. |
| **4. Tee↔badge association composite plus traced basket child.** Owner: association calculation module and graph/YAML sample. Preserve raw paths, collapsed/scored alternatives, selected one-to-one locks, abstentions, and then invoke Task 2’s `traceBasket`. | Tasks 1–2; Task 3 only if recovered tees feed this set. | Competing locks yield ranked alternatives, named abstention, and an immutable partial trace instead of a fabricated basket. | Association silently force-matches a tiny positive score, or an `unknown` basket becomes a claimed endpoint. |

## Compatible construction sets

- **Recovery-only:** Tasks 1 + 3. It can consume S1 ownership/muted/remaining outputs and return one ordinary composite result per missing badge; it needs no nested graph syntax.
- **Association trace-only:** Tasks 1 + 2 + 4, using visible/recovered tees already supplied by a fixture.
- **End-to-end:** Tasks 1–4, with S1’s separate badge ownership source as the immutable subtraction provenance. Keep recovery and association as separately named calculations; connecting outputs is not permission to merge their semantics.

## Strong checkpoints and rejected material

- `43829313870fc0b792782e5ce751b924de07f684`: existing S1 PQL/YAML checkpoint. Its ordered `Calculations` and `into` addresses are the nearest usable authored-composition precedent.
- `fa44a4505d9aafbf6d2d21a12400298edb7fa96d`: wires white recognition and separate badge ownership/muted/remaining outputs through PCR.
- `b5a6ae040147b488bc44ea94c6303296b2ecde78`: explicit unrun review proof. Treat its compiler/runner as a fixture and a demonstrated design intent, not runtime evidence.
- Rejected: predecessor-basket-radius discovery; whole component/chrome drops; basket bbox ownership; interpreting a badge digit as a tee shard; loop-order ambiguity resolution; and count-only assignment success. The historical “phantom tee” is explicitly completion-only and default OFF, not recovery evidence.

No new code or execution was performed for this research lane.
