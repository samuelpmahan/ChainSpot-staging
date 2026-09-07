# S0–S2 infrastructure baseline

Evidence: source inspection, not execution. ChainSpot base fa44a4505d9aafbf6d2d21a12400298edb7fa96d;
Mermaid proof published at b5a6ae040147b488bc44ea94c6303296b2ecde78. Its Dash run/render is a separate receiving-agent task.

## Existing code and concrete seams

| Surface | Implemented | Gap / task implication |
|---|---|---|
| exec/pql.ts | Named functions, explicit named address inputs, args, ordered Ticks, synchronous invocation | Direct result bindings and awaiting are only in the experimental runner. Shared path must accept old YAML and the agreed graph representation. |
| S0/exp/mermaid-pcr/compiler.ts | Two independently compiled graph documents; explicit fn vs px binding; occurrence IDs; ordered acyclic subset | Prototype rejects forward declarations rather than scheduling. Keep that boring constraint until real composition needs more. |
| S0/exp/mermaid-pcr/runner.ts | Awaits actual values; occurrence-local map; returned records preserve prefix/failure | It records top-level graph calls, not arbitrary child calls; it is a second experimental interpreter, not shared PQL integration. |
| exec/stage.ts | Fork per variant, prepare, run, compare; variant board returned in each result | Pipeline must choose and pass the requested successful board. Overrides keyed by fn address affect every occurrence. |
| stages/S1/contract.ts | Existing pipeline entry invokes clean implementation | Explicit YAML selection is not connected through this entry. |
| stages/componentPxC.ts | px.image.cropped, px.components.masks, px.components | New S1 public outputs do not provide this consumer representation by themselves. Any projection needs to preserve masks/label identities and prove equivalent geometry inputs. |
| stages/S2/clean/Basket.ts | detectFamily, findShellFamily, findPx; last calls registered fn once per shell member | Per-object calls and composition already exist. Record actual child invocation and object identity instead of inventing graph-level foreach first. |
| stages/S2/clean/index.ts | Three Ticks, operation/runtime/binding tables, manual PCR composition | Existing duplication is the authoring-kit target; retain named functions and algorithm semantics. |
| exec/board.ts; exec/gateway.ts | Board traffic tracking plus declared calculation bindings/body hash | Binding a function is not proof it executed. Current hash explicitly excludes called helpers/constants/templates/assets. Fork shares value references. |
| src/lib/parts-inspector/parts.ts | Traversal recognizes component/mask | pixel-set and richer relations need shared material traversal; do not require a bespoke script per Stage. |

## Constraints from the inspected implementation

- Existing S2 reads bright/dark component fields, not px.remaining.afterBadges.
  Adding badge exclusion to S2 is an algorithm change, not transparent compatibility.
- The Mermaid S1 proof keeps all 15 original S1 Calculation occurrences plus an explicit raster adapter.
  Existing preparation also seeds the raster; this duplicate shape conversion is visible, not a second detector.
- FullImage is direct run material; it remains referenced in returned inspection records.
  No explicit FullImage address or separate cache in generated S0. No assertion that its memory disappears early.
- The bounds output is the actual StripChromeResult, including insets/proposal metadata.
- Owned component union, additional muted pixels, full bbox exclusion query and remaining pixels have different meanings.
- Only graph-level invocation failure has a preserved record in the prototype. Shared PQL and Stage errors still need the same behavior.

## Recommended foundational units (provisional until the later-stage reports arrive)

1. Dash proof + actual rendered inspection (already handed off).
2. One shared async/direct-result execution path preserving old YAML and failure prefix.
3. Named nested Calculation call records, per-object occurrence identity and actual traffic.
4. Selected Stage adapter + public output declarations + one explicit compatibility projection into existing S2.
5. Shared traversal/materialization for actual Parts, objects, measurements, relations, rejected/empty results.
6. Define Calculation once + stage-local collection; check/explain derives resolved wiring from composition.
7. Occurrence-level experiment alternatives; explicit selection, immutable input expectations, identity limits.

Do not block S1 integration on graph shorthand, cache optimization, dependency scheduling,
full schemas or product code generation. Keep those separately identifiable if useful.
