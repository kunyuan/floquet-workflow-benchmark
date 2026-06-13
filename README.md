# Floquet Workflow Benchmark

A harbor-format benchmark suite testing whether an agent can **reproduce and
apply the Floquet effective-Hamiltonian workflow** (workflow family #1069:
define a time-periodic H(t) → choose a Floquet method → construct the
effective Hamiltonian / Floquet operator → compute quasienergies and states →
evaluate observables), built from the published literature of that family.

## Structure: four tracks, one verifier type each

Each record inside a track exercises the same workflow facet; answers may be
numbers, integers, or closed-form formulas — each answer type has a typed
verifier.

| Track | Facet | Answer type |
|---|---|---|
| `B1-topo-invariants` | symmetry class + gauge-invariant diagnostics | integers |
| `B2-quasienergy` | core numerics: build & diagonalize the Floquet operator | dimensionless quasienergies / closed forms |
| `B3-critical-points` ★ | **flagship: the full workflow loop + parameter scan** | critical drive parameters |
| `B4-eff-coupling` | analytic high-frequency expansions | dimensionless coupling ratios / closed forms |

B3 is the end-to-end metric; B1/B2/B4 decompose the capability so failures
localize to a segment of the chain. Every track ships a **train** split
(worked examples for skill distillation) and a **validation** split
(question-only, generalization test), stratified by model family.

## Layout

```
data/workflow_preamble.md    # Q module 1: the workflow description (shared)
data/environment_setup.md    # Q module 2: environment & answer protocol (shared)
tracks/<track>/records.jsonl # canonical records (Q module 3 + answer + verifier + provenance)
tasks/<track>/<id>/          # materialized harbor tasks (instruction.md = assembled Q)
verifiers/verify.py          # typed verifiers (integer / scalar / quasienergy set / formula sampling)
scripts/                     # assemble_prompt, materialize_harbor, splits, validation, scoring
```

Prompts are assembled deterministically (`scripts/assemble_prompt.py`);
`records.jsonl` is the single source of truth.

## Verification

```bash
python verifiers/verify.py --record <record.json> --pred <pred.json>
python scripts/validate_records.py    # schema + gold self-check + split-leak check
python scripts/score_run.py <run_dir> # score a solve run, per track x split
```

Formula answers are verified by numerical sampling equivalence (complex
values, folding, and finite series supported). Tolerances are calibrated to
each gold's significant figures.

## Provenance

Gold values trace to published papers; records carry the paper DOI (where
available), a verbatim source excerpt, and opaque provenance references
(`paper_ref` / `source_ref`). Records flagged `needs_original_paper` await
verification against the original publication and are excluded from scored
use; see `quality_report.md` for the honest state of the suite, including
known gold disputes and per-item cold-solve difficulty metadata.

## Status

Initial release: 41 records (B1 12 / B2 12 / B3 10 / B4 7 — B4 is marked
*preliminary*). Baseline solve runs and the QA history are documented in
`quality_report.md`.
