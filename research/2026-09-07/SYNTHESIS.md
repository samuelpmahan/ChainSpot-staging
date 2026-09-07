> Scope superseded by the accepted [PLAN.md](../../PLAN.md). This document preserves the earlier infrastructure-first research synthesis; jira.json now covers the full S0–S7 delivery.

# ChainSpot infrastructure synthesis — 2026-09-07

Three Terra source-research lanes returned and were reconciled immediately with the S0/S1 prototype and existing S2. No new algorithm run, parity test or rendering was performed in this research pass. The separate Dash Refine agent's first job remains run/render, then redo the checklist with Sam.

## The conclusion

The later code needs a small shared execution/inspection kit, not a richer control-flow language. Existing bounded loops can stay in named composite functions. What must become automatic is the real invocation record, source/publication links, selected Stage handoff, and faithful default presentation.

**A Luna supplies:** named Calculations (including ordinary composition/loops), stage-local collection, readable composition, explicit public outputs, and domain result meanings. **Machinery supplies:** registration/default resolution, invocation/await/direct-result passing, parent/item occurrence records, output publication, selected-board handoff, and common check/explain/materialization.

Calculation definitions own function inputs/defaults. Composition owns bindings/output addresses. Stage boundaries own required outputs. Remove duplicated bookkeeping, not these distinct decisions.

## What each lane changes in the plan

| Lane | Concrete existing pattern | Infrastructure consequence |
|---|---|---|
| Visible tees | S3: components + badges → rings → family → exact pixels; findPx invokes once per accepted member | Record actual nested calls and empty collections. Use the existing calculation sequence as a fresh-author pilot. |
| Recovery/association | Global remnant search + constrained fit + alternatives; one-to-one locks; per-lock basket traces that can remain partial | Ordinary composite result values carry decisions and reasons. Shared keyed child invocation records keep per-lock work inspectable. Unknown result differs from execution failure. |
| Geometry/paths | Geometry inventory can ABSTAIN; whole-set matching consumes existing candidate edges; finite pair swaps consume caller-built segmentation | Composite outputs and explicit shared intermediate inputs suffice. Selection remains separate from evidence; loops and solver stay algorithm code. |

## Compatibility is where the easy-looking work can change the algorithm

- New S1 publishes `px.badges.objects`, `px.badges.px`, `px.badges.muted`, and `px.remaining.afterBadges`.
- Existing S2 requires `px.components` and `px.image.cropped`. It does **not** consume remaining-after-badges. Shape compatibility must use actual selected-run Parts without rerunning old detection or silently adding exclusion behavior.
- Existing S3 additionally requires old `px.badges`, specifically `badge.has.mute.px`. The correct compatibility source is the full badge exclusion query. Additional `px.badges.muted` alone omits explained badge pixels and is insufficient.
- Historical G3 teeFamily is a refinement of legacy `tees`, preserving component/recovered passthrough and original-image Y alignment, with a fill criterion. Clean S3 is cropped-frame visible-ring construction using major/minor/area. A projection cannot quietly make these equivalent.
- Badge full-bbox exclusion is an explicit ownership rule here. Basket bbox is still geometry, not owned ink. Preserve their different meanings.

## Recommended sequence and actual parallelism

1. **PCR-001:** receiving Refine agent runs and renders full Dash, repairs bounded blockers, then revises the checklist with Sam. The published prototype is unrun.
2. **PCR-002/003:** one execution owner consolidates the prototype into shared PQL and records actual nested named calls. It may begin from the source evidence while Dash Refine runs; incorporate Refine results before accepting the shared path.
3. After the common record/output contract is available, **wiring (PCR-004/005)** and **inspection (PCR-006)** can proceed in parallel with disjoint files. Shared executor edits stay with one owner.
4. **PCR-007:** demonstrate selected S1 → existing S2 with visible material, push-review and land the accepted exact revision after Sam chooses the target. Do not wait for authoring conveniences.
5. **PCR-008/009/010:** simplify definition/registration, occurrence overrides, and check/explain against that real seam. These tasks share core files, so the same execution owner sequences their edits.
6. **PCR-011–014:** selected visible-tee, recovery, straight-geometry and assignment pilots prove the kit supports real later-stage work. These are algorithm/source-policy choices, not already-approved automatic ports. Each has its own stopping test.
7. **PCR-015** is a deferred historical bounded-refinement/reuse pilot, not a reason to build an automatic cache or scheduler now.

## Reconciliation decisions

The reports initially differed on adding a declarative foreach and on manual child diagnostics. Reconciliation: **keyed child testimony is required; new loop syntax is not yet required.** Use shared named invocation inside an ordinary loop first. Domain fields such as pair distances/rejection reasons remain ordinary outputs; they must not become per-algorithm copies of generic tracing.

Arbitrary result objects already flow through the prototype. Relations/confidence/unknown outcomes need definitions and honest inspection, not mandatory universal schemas. Explicit `into` outputs go to PxC; direct intermediates remain run-local; `RunRecord` is testimony rather than the downstream consumer API. Version/reference discipline must keep earlier source meaning intact without duplicating every raster in memory.

## Source selection and evidence limits

- Current reference: S1 `fa44a45`; unrun Mermaid proof `b5a6ae0` (descends from S1).
- S3 reference: `ac369f1`; legacy tee-family reference: `7fbd6b9`; recent Dash/G5 reference: `b9d05cd`.
- P5/P6 `b1f4c833`, `d47af552`, `b8452b58` are **August 14 historical dependencies**, not newly validated September algorithms.
- Historical ledger/receipt statements are not fresh reproduced evidence. No automatic Gate→Stage mapping, source promotion or correctness claim is made.

The full source paths, bounded ownership, dependencies, demonstrations and falsifiers are in `jira.json`; the individual reports retain their inspected source checkpoints. This file tracks the work. It does not create another project-management service.
