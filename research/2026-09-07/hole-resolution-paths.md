# Hole-resolution paths: G5–G7 research for PCR composition

**Status:** read-only synthesis, 2026-09-07. The local S0/S1 Mermaid proof is written but unrun; no runtime/parity claim is made here. `S5` and historical `G5` are not treated as equivalent numbering.

## Strongest source evidence

| Source | Concrete implementation | What it establishes |
|---|---|---|
| [`b5a6ae0`](https://github.com/samuelpmahan/ChainSpot/commit/b5a6ae040147b488bc44ea94c6303296b2ecde78), `packages/alg/src/stages/S0/exp/mermaid-pcr/{compiler,runner}.ts` | `compileMermaidPcr` accepts named edges from an earlier `fn` result or a published `px`; `executeMermaidYaml` holds `fn` results in a run-local `Map` and puts only `into` outputs into PxC. | Direct result reuse is already enough for a calculation chain in one PCR. It is *not* an externally addressable materialization. |
| [`b9d05cd`](https://github.com/samuelpmahan/ChainSpot/commit/b9d05cdd26b352641f582c53a52d1ae2712d8271) (2026-09-06; last-week branch), `features/st.straightTest.ts` | `measureStraightGeometry` calculates chord fraction `f`, perpendicular displacement, axial and directional residuals; `straightTestUnit.run` reads `badges`, `tees`, `baskets` and emits `straightProposals` plus overlay/trace testimony. | The current G5 proof is geometry-only and default-OFF. Blind mode deliberately returns `ABSTAIN`, rather than promoting soft scores into truth. |
| [`b1f4c833`](https://github.com/samuelpmahan/ChainSpot/commit/b1f4c833d32426d3094c93403af5055057ea63f1) (contains 2026-08-14 P5 dependency), `src/lib/autoAnnotation/p5SparseAssignment.ts` | `deriveP5SparseAssignment` constructs a rectangular sparse cost matrix from P3/P4 candidate edges, uses Hungarian assignment, rejects sentinel results, and retains status/reason/candidates/perfect-matching testimony. | Older dependency: one-to-one ownership is a whole-set operation after candidate generation. Unknown/unresolved must survive; a solver result cannot silently become a hole fact. |
| [`d47af552`](https://github.com/samuelpmahan/ChainSpot/commit/d47af552693bfe8cc2e2efecc62e1d38a9aaebd9) and [`b8452b58`](https://github.com/samuelpmahan/ChainSpot/commit/b8452b589621287811e413a57a493082891b0d71) (both 2026-08-14 older dependencies), `p6LowParBasketAssignment.ts` | P6 first solves only pre-existing valid basket edges. P6.2 evaluates eligible 2-hole swaps, requires all four ribbon distances and at least `MIN_RIBBON_IMPROVEMENT_PX`, then applies non-overlapping swaps strongest-evidence-first. `RibbonMassSegmentation` is built once by the caller and passed to P4 and P6.2. | Bent-path refinement is a bounded, evidence-gated correction over prior candidates. The reusable warm intermediate is explicit input data, not ambient cache state. |
| [`b9d05cd`](https://github.com/samuelpmahan/ChainSpot/commit/b9d05cdd26b352641f582c53a52d1ae2712d8271) (2026-09-06; last-week branch), `experiments/dashs-track-edge-sensing/matrix-review` | Dash branch preserves 72 matrix outcomes, 20 missing-seed rows, connection/spacing checks, and resumed H18 measurements. | Dash evidence is valuable to calibrate and falsify a path hypothesis, but it is an experiment archive, not an execution/data contract. |

The requested `b5a6ae0` checkpoint (2026-09-07) is a descendant of local `fa44a45`; it is absent from the shallow local object database. Its remote commit and files were inspected directly.

## Actual algorithm sequence and state boundaries

1. **Inputs:** identified badge, measured tee, measured basket, plus their provenance and confidence.
2. **G5 straight testimony:** calculate geometry for each proposed triple. `measureStraightGeometry` returns nullable measurements for absent/degenerate evidence; `evaluateStraightTestCandidate` records identity gates as `PASS`/`FAIL`/`UNKNOWN`. In blind mode it returns `ABSTAIN`; only explicitly `TRUTH-TAINT`ed canonical locks can be marked `PROVISIONAL`.
3. **Candidate ownership:** historical P5 keeps each tee's candidate hole numbers and axis-error costs. A resolved P4 edge narrows the row to one candidate; otherwise P3 candidates survive. Hungarian selection operates on the complete matrix, after which disallowed/sentinel choices and duplicates become `unresolved` with `noValidAssignment`.
4. **Basket assignment:** P6 preserves P4 locks, scores only remaining valid candidate basket edges, runs one global assignment, then reports `p4Locked`, `lowParAssigned`, or `unresolved`. It does not invent edge candidates.
5. **Bent correction:** P6.2 considers only a two-cycle where both alternate P6 candidate edges already exist and have scores. Missing ribbon component/distance is a skip, not inferred evidence. It evaluates all eligible pairs, orders them by evidence improvement, and consumes a hole at most once. This is finite: (O(n^2)) pair enumeration plus one selection pass; no convergence loop.
6. **Materialization/testimony:** historical output contains assignments, candidates, lock/state/reason, duplicate/disallowed counts, per-pair distances/costs/applied flag, timings, and changed holes. The local Mermaid runner records per-calculation status/inputs/output in `RunRecord`, and writes every declared `into` output into PxC; only un-published function results remain run-local.

## Fit to the current Mermaid compiler

### Reuse and addressing

- A direct `fn` result may feed multiple later `fn` inputs in declaration order. This is the right mechanism for an intermediate such as `{ candidates, rejected, unknown, measurements }` **inside one composition**.
- Only `fn --> px.*` creates a stable PxC address. The compiler permits at most one published PxC output per function, so a multi-part output should be one typed composite published once, followed by explicit extraction functions when independently consumed. Do not use `RunRecord.output` as a consumer contract; it is interpreter testimony.
- Existing G5 uses board-slot arrays (`badges`, `tees`, `baskets` → `straightProposals`). The corresponding PCR input/output Parts should be typed object arrays, not per-object named PxC addresses.

### Loops, children, and budgets

- No new Mermaid loop syntax is needed for per-hole Cartesian candidates, Hungarian solve, or the P6.2 pair pass. Put each bounded loop inside a named calculation function and return its full typed result/testimony. That keeps authored math and readable composition in one place.
- A function's internal helper calls are not visible as separate `CallRecord`s. When a child is a named Calculation in the authored composition, shared machinery must record it as a named child Calculation call with bindings, status, and result reference (a PxC address when it publishes one), just as it does any other calculation. Domain data such as `pairDiagnostics` remains in the parent's typed result, but must not be repurposed as repeated hand-built generic tracing.
- The only present iteration budget worth carrying forward is the algorithm's explicit, documented bound: candidate counts and unordered pair enumeration. A convergence/retry syntax is unjustified by the cited G5/P6 code.

### Semantic states

`rejected`, `unknown`, and `inferred` must remain distinct. Recommended hole-level state vocabulary is `measured`, `candidate`, `rejected(reason)`, `unknown(reason)`, `assigned`, `unresolved(reason)`, and—only where an explicit recovery policy permits it—`inferred(provenance)`. Neither a high score nor a completed matching may convert unknown identity into measured identity. This matches G5's blind abstention and P5/P6 sentinel rejection.

## Bounded pilots: one infrastructure proof, then source-policy algorithms

### Infrastructure pilot needed before algorithm selection

1. **PCR typed-composite publication and extraction proof**
   - **Own:** `packages/alg/src/stages/S0/exp/mermaid-pcr/{compiler,runner,proof}.ts`, `experiments/mermaid-s0-s1/` only.
   - **Depends on:** `b5a6ae0` run/render baseline.
   - **Change:** prove one calculation can direct-feed two named child Calculations and publish one typed composite Part; add two explicit extraction calculations for independently addressable children. Shared machinery must record producer and named children as Calculation calls with status, bindings, and result reference (a part address when declared) in the receipt.
   - **Acceptance:** a Dash S0/S1 run shows one producer call, both named children receive the same logical value, every named calculation has a shared trace record, and only declared `px.*` outputs are consumed across composition boundaries.
   - **Falsifier:** an extraction requires recomputation, a consumer reads `RunRecord.output`, or typed-array/shared-identity output cannot be represented without a hidden side channel.

2. **G5 typed triple inventory algorithm pilot (no selection)**
   - **Own:** a new S5/G5 experimental composition and its contracts under `packages/alg/src/stages/S5/exp/` (or the stage chosen by the owner); no reuse of `G5` as a directory name.
   - **Depends on:** task 1, typed Parts for badge/tee/basket evidence, and source-policy selection; this is not an automatic mapping from historical G5 to a new S5 stage.
   - **Change:** one `fn.g5.inventoryTriples` consumes the three arrays and emits `{ proposals, rejected, unknown, counts }`; each proposal uses the historical `f`, `dPerpPx`, axial/directional residual definitions and per-input provenance.
   - **Acceptance:** receipt has an entry for every eligible badge, counts equal the emitted arrays, missing endpoints/angle are `UNKNOWN`, and blind mode selects no ownership.
   - **Falsifier:** an unmeasured endpoint receives a hard verdict, a filtered candidate has no reason, or the function needs graph-level per-hole loop syntax.

3. **One-to-one assignment algorithm pilot with explicit candidate matrix testimony**
   - **Own:** `packages/alg/src/stages/S5/exp/hole-resolution/{assignment.ts,contract.ts}` and its experimental composition.
   - **Depends on:** task 2 and explicit source-policy/candidate-edge selection; it is a pilot, not essential infrastructure or an automatic stage mapping.
   - **Change:** port the P5/P6 shape, not its old thresholds: candidate rows, allowed-edge matrix, Hungarian result, sentinel rejection, duplicate check, and `{ assigned, unresolved, rejected, matrixSummary }` testimony.
   - **Acceptance:** duplicate baskets/hole labels cannot be materialized; a valid perfect matching is reported; any solver-selected forbidden edge becomes unresolved with a reason.
   - **Falsifier:** assignment creates a candidate edge, hides a duplicate, or loses the source evidence/reason for an unresolved row.

### Later, after source-policy selection and G5-pilot acceptance

4. **Bounded bent-path two-cycle algorithm pilot**
   - **Own:** `packages/alg/src/stages/S6/exp/hole-resolution/{ribbonPart.ts,swapAdjudicator.ts,contract.ts}` and its composition.
   - **Depends on:** source-policy selection, a measured ribbon/material Part, and task 3 assignments; it must consume the exact same segmentation Part as its upstream path evidence. It is not an automatic G6-to-S6 mapping.
   - **Change:** reproduce P6.2's eligible-two-cycle rule, null/unknown skips, evidence-improvement threshold supplied by the chosen experiment contract, strongest-first non-overlap selection, and per-pair testimony.
   - **Acceptance:** every applied swap has both existing alternate candidate edges, four finite distances, positive documented improvement, and no hole appears in more than one applied pair; receipt exposes applied and skipped pairs.
   - **Falsifier:** it recomputes segmentation, creates new basket edges, needs unbounded convergence, or mutates a P4/G5 lock.

## Recommendation

Start only task 1 on the frozen Dash input (`chainspot-corpus@2b5913d3f1f6d8f97b0324721a4c5201bd3ed819`, `dev/DashsTrack/DashsTrack-full.jpg`). Tasks 2–4 are algorithm pilots after the owner selects their source policy and semantic contract; none automatically maps a historical G-number to a new stage. There is no evidence for a generic compiler, scheduler, cache, or loop-language redesign before these falsifiers are tested.
