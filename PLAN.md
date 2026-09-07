# Accepted plan: canonical image through numbered hole paths

Accepted by Sam on 2026-09-07 after the full flow was explained. This is the saved
planning baseline. Implementation can refine it through observed results and
explicitly recorded changes. Acceptance of this plan is not a claim that the
algorithms already run or are frozen.

## Outcome

A numbered hole with tee geometry, basket endpoint, path geometry and an
inspectable account of observed versus inferred material—or a specific unresolved
result retaining the useful partial work.

## Complete flow

| Step | Computation | Public handoff |
|---|---|---|
| S0 Intake | Decode once, determine crop, apply it; retain coordinate mapping. | Canonical pixels and crop/frame mapping. |
| S1 Badges | Black/white components, badge assembly, number recognition and declared ownership. | Numbered badges; explained pixels, additional muted pixels, full exclusion query and remaining pixels. |
| S2 Baskets | Family selection, shell association, exact constituent pixels and endpoint geometry. | Basket candidates, pixels and tips, with rejected/incomplete material. |
| S3 Visible tees | Ring candidates, family classification, exact pixels, centroid and orientation. | Visible tees plus considered/rejected candidates and reasons. |
| S4 Tee–badge and recovery | Measured tee direction yields badge candidates. Missing tees use remaining fragments and explicit occlusion constraints; retain ambiguity. | Relationships, recovered geometry and unresolved cases with provenance. |
| S5 Straightness | Evaluate candidate geometry against tee–badge direction; distinguish straight, bent and insufficient evidence. | Straight-hole candidates and cases needing path evidence. |
| S6 Straight-hole resolution | Evaluate plausible baskets along established direction; accept supported local relationships, retain conflicts. | Resolved straight holes and unresolved endpoint alternatives. |
| S7 Paths and bent holes | Follow image-supported routes, compare endpoint connections, resolve ambiguity using path evidence. | Hole paths, endpoint relationships, alternatives and unresolved sections. |

Stage labels name the accepted logical plan. Historical G/P numbering is not an
automatic mapping and cannot justify substituting one implementation for another.

## Pathfinding composition

1. **Build support.** Start from the canonical image. Existing
   `computeRibbonSupport` samples widths/orientations and returns support strength
   plus preferred direction. Preserve source/frame and parameters so newer Dash
   support experiments can be compared at this same boundary.
2. **Represent occlusion.** Treat any inferred continuation behind badges as an
   explicit derived field with assumptions and changed cells. Existing
   `patchBadgeOcclusion` is reference code, not permission to mutate the raw support
   Part invisibly. Basket ink and badge footprint remain different ownership rules.
3. **Build cost.** Convert support to traversal costs with `buildSupportCost` or
   the selected equivalent. Publish the relationship and arguments; show the field.
4. **Search and reuse.** Existing `routeBadgeLegs` runs a bucket-queue flood once
   per badge, then reconstructs paths to candidate tees and baskets. Keep that
   reuse explicit; do not rerun the search for every tee–basket pair. Preserve
   reachability, path coordinates, distance/cost and actual named invocations.
   Existing flood builds its cost internally; expose/reuse that value if split into
   separate Calculations, without accidentally building cost twice.
5. **Assemble and assess.** Combine tee/badge/basket legs with endpoint geometry
   and path measurements. Existing `makeRawPairs`/`makeRawPairEvidence` provide a
   concrete source boundary. Reachability alone does not establish the correct hole.
6. **Resolve and refine.** Preserve strong local decisions; arbitrate competing
   assignments over retained candidates. Refine accepted paths, exposing unsupported
   sections and alternatives. Historical two-cycle swaps are one optional refinement
   technique, not the definition or prerequisite of pathfinding.

Pathfinding may begin when useful local anchors exist. Its evidence feeds unresolved
S4–S6 decisions; do not gate every route behind global endpoint perfection. Use a
bounded re-evaluation of affected candidates with recorded reasons, not an unbounded
retry-until-18 loop.

## Authoring and execution

Each step follows the same pattern:

Calculations + readable composition + declared outputs → actual execution →
materialized inspection → downstream handoff.

Ordinary functions own algorithmic loops and composition. Shared machinery handles
registration/defaults, awaiting/direct-result reuse, actual keyed child invocation
records, source/publication links, variant selection and inspection. Domain results
carry alternatives, rejection reasons, measurements and decisions as ordinary values.
New graph control-flow syntax is optional until a real case needs it.

Existing S2 needs component-field compatibility. Existing S3 also needs old badge
objects' full mute footprint; new additional muted pixels alone cannot satisfy it.
Legacy coordinate/family/recovery differences must remain explicit through conversion.

## Delivery order

- First: receiving agent runs/renders the published Dash S0/S1 proof, then revises
  the checklist with Sam. Fix bounded blockers and keep moving with useful results.
- Build shared execution/recording, then parallel Stage wiring and inspection.
- Demonstrate S1→existing S2 and land the accepted checkpoint without waiting on
  optional authoring conveniences.
- Finish the full S2–S7 path through bounded stage tasks. Build path support/search
  alongside later object-stage work using explicit fixtures/available anchors.
- Each useful checkpoint includes exact code, input, invocation, rendered material,
  known gaps and a pushed Git handoff. Refine starts fresh from that packet.

`jira.json` is the task/dependency state for this plan. The original Terra reports
remain source evidence; the earlier infrastructure-only synthesis is historical and
superseded in scope by this accepted plan. No new management service is required.

## Source and acceptance boundaries

Implementation references include ChainSpot `fa44a45` (`ribbon.ts`, `routing.ts`,
`measure.ts`, `assignment.ts` under `packages/alg/src/detectors/threeFactor/`),
S3 `ac369f1`, legacy G3 `7fbd6b9`, Dash `b9d05cd`, and unrun Mermaid proof `b5a6ae0`.
Exact references and known limits are retained in Jira and the research reports.

Good enough to inspect and continue is a valid intermediate checkpoint. A complete
assignment count, green comparison, or rendered line alone cannot prove identity,
ownership or path correctness. Sam supplies semantic/visual acceptance; ordinary
implementation choices should not repeatedly return to Sam for permission.
