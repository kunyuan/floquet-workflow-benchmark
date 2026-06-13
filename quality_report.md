# Quality Report — Floquet Workflow Benchmark (build finalized 2026-06-13)

## Baseline solve run + scorecard (40/41; 1 B3-train item still computing)

A question-only baseline solve (sonnet-tier agents, ~10–15 min/task, python
allowed) was scored with the real verifiers. This run doubled as a 4th QA
layer — it surfaced bugs that authoring, machine-rescan, and review all
missed.

| Track | train | validation | nature |
|---|---|---|---|
| B4 eff-coupling | 4/4 | 3/3 (100%) | canon high-frequency formulas — no discrimination at this tier (as predicted) |
| B2 quasienergy | 6/7 | 1/5 | small-Hilbert-space closed forms solve; hard-numerics + disputes fail |
| B1 topo-invariants | 3/7 | 1/5 | depressed by 5 gold disputes (below), not pure difficulty |
| B3 critical-points ★ | 1/6 | 2/4 | flagship; hardest by design (heavy-numerics scans resist cold solve) |

Difficulty gradient B4 > B2 > B1 ≈ B3 matches the design intent: canon
formula tracks are baseline-solvable; the flagship full-workflow track and
non-generic-integer items resist.

### Verifier hardening found by the run
- `formula_equivalence` now normalizes `^` → `**` (agents write caret for
  exponentiation; Python read it as XOR and errored). Pure false-negative;
  fixed. Lifted B2 from 4→6 (train) and 0→1 (val) with no gold change.

### Gold disputes surfaced (flagged `needs_original_paper` + `gold_dispute`,
excluded from scored use until adjudicated)
- `flq-b1-tbg-circpol-W-spectral`: 3 independent solvers get W=+1 vs gold −1
  (spectral-winding sign convention under right-CP).
- `flq-b1-kicked-ssh-chern2`: 4 independent methods give C=0 for the φ=0
  model; φ=π/2 (not the question's params) gives C=1 — likely a
  question-parameter or gold error.
- `flq-b1-bbh-n0-0-npi-4`: N_0, N_π match gold; V_R (0 vs 1) and
  corner_states (4 vs 16) disagree.
- `flq-b1-dqs-floquet-1d-nu0-nupi`: baseline OBC spectrum gives (0,1) with
  explicit π-edge-modes vs gold (1,1).
- `flq-b2-graphene-floquet-freq`: baseline mass term carries vF^4 vs gold's
  bare λ^4 (possible vF-absorption convention).
Corroboration from redundant solver runs (independent re-derivations of the
same two tasks): `kicked-ssh-chern2` confirmed C=0 a **third** time (Berry
curvature odd in θ ⇒ exact cancellation for φ=0) — the gold of 2 is almost
certainly a question-parameter error (φ should be ≠0). `delta-ad-zero-threshold`
is NOT a gold error: the gold 0.782 was independently reproduced; the question
merely fails to disambiguate which of two thresholds (0.782 vs 1.165) is asked
— a question-clarity fix.

These are the highest-value output of the run: independent recomputation
(QA-6) had "confirmed" several via the source formula / region logic, but
genuine numerical re-derivation from H(t) disagrees — i.e. QA-6's
formula-faithful check cannot catch a wrong *premise*; only an independent
build of the model can. Adjudication needs the original papers.

### Genuine (non-dispute) hard fails — the good kind
- `flq-b2-sq-well-osc-barrier`: solved to 3.6% but tol 0.1% (metastable
  resonance convergence) — the intended difficulty.
- B3 heavy-numerics (graphene-antidot, kicked-Harper, 4D-QHE, photonic-CDT,
  Weyl-node): cold-solve resists within budget. Antidot pred was transcribed
  from the dead solver's own results_raw.json (agent self-flagged
  non-converged).
- `flq-b2-pxp-ca-vacua`: solver returned ε in radians, not the dimensionless
  ε/ω_eff the gold uses — borderline question-units clarity; left as a fail.



## Final state (supersedes the inventory below where they differ)

41 records / 4 tracks (B1 12, B2 12, B3 10, B4 7), all materialized as harbor
tasks (`tasks/`), validator PASS. Questions are assembled from three modules
(workflow preamble + environment protocol + per-paper part) via
`scripts/assemble_prompt.py`. Post-build hardening applied:

- **De-leak rewrite**: ~45% of first-draft questions contained the source
  formula/criterion; all stripped, replaced with physical definitions.
- **Convention pinning**: Chern/winding sign conventions stated explicitly
  (fixed two false-survival items); two B2 type-drift records restored under
  the workflow-uniform contract; complex values normalized to _re/_im.
- **Tolerance calibration**: rel_tol = 2.5× gold half-ulp, capped 10%; two
  B3 golds (1-2 sig figs) flagged needs_original_paper for more digits.
- **Cold-solve probe (2 rounds, sonnet-tier, question-only)**, results in
  each record's `metadata.cold_solve` with question hash:
  - B1 5/12 cracked, B2 7/12 (incl. 2 round-1 results), B3 4/10, B4 4/7.
  - Survivor profile: heavy-numerics scans (B3 core), non-generic integers
    (B1), convergence-demanding resonances (B2), paper-specific
    composite couplings (B4).
  - Cracked profile: mostly `computed` on clean questions = baseline-solvable
    small-Hilbert-space systems (legitimate workflow execution by the probe),
    plus genuine canon (Bessel-zero CDT, J0 renormalization). Per owner
    principle, no items were moved between splits.
- **B4 is marked `preliminary`**: 7 records (3 validation) is below the
  ≥10/≥4-5 sizing floor and its canon share is the highest; do not force-fill.
- Open queue before scored use: per-record H(t)-spec faithfulness review;
  4 needs_original_paper golds (δ-scatterer ×2 metadata mismatch, 2
  low-precision golds); independent recomputation of formula_derived golds
  (QA-6); Weyl V₀ sign-convention check.

Built from the knowledge-graph service knowledge graphs of a curated literature workflow atlas cluster #1069
(191 papers; 147 graphs recoverable, 44 empty). All records drafted by model
agents from the knowledge-graph service node content under explicit integrity rules; every record
carries `source_node_id` + verbatim `source_excerpt`.

## Final inventory: 41 records

| Track | train | validation | gold: paper_reported | gold: formula_derived | needs original-paper check |
|---|---|---|---|---|---|
| B1 topo-invariants | 7 | 5 | 10 | 2 | 0 |
| B2 quasienergy (formula track) | 7 | 5 | 1 | 11 | 0 |
| B3 critical-points ★ | 6 | 4 | 9 | 1 | 2 |
| B4 eff-coupling | 4 | 3 | 0 | 7 | 0 |
| **total** | **24** | **17** | **20** | **21** | **2** |

`python scripts/validate_records.py` → PASS (schema complete, every gold
passes its own verifier, no duplicate ids, no model-family overlap between
splits).

## Gold-provenance policy (evolved during the build — record of decisions)

1. Initial strict pass (gold must be explicitly stated in node text) yielded
   only 19/70 records; the flagship-quality skips fell into three classes:
   misclassified papers (~1/3, correctly rejected), formula-without-pinned-
   parameters (~1/2), genuinely qualitative conclusions (~1/4).
2. A cross-paper sweep over ALL conclusion nodes of all 147 graphs (not just
   each paper's headline result) recovered +4 B3 records but **0 B2 records**:
   quasienergies are essentially never reported as literal numbers in the
   literature — only as closed-form formulas, figures, or symbolic sector
   labels (E=0, E=π).
3. **B2 was therefore redefined as a formula track** (owner decision):
   gold = closed-form formula stated verbatim in the the knowledge-graph service node (the paper's own
   result) evaluated at owner-pinned parameters inside the stated validity
   regime. The formula is source_verified; the evaluation is mechanical and can
   be cross-checked by independent U(T) numerical evolution (the atlas's own
   evaluation protocol) — planned as a pre-release selfcheck. The tested agent
   never sees the formula; difficulty is unchanged.
4. B1 recovery used phase-diagram pinning: a parameter point fixed strictly
   inside a region whose invariant and boundary formulas are both explicit in
   the node (2 records; 3 candidates rejected because the region→integer map
   was not explicit).

## Known issues / review queue

1. **Single-pass agent drafting.** Every record needs one human/agent review
   of H(t)-spec faithfulness before scored use (planned anyway as part of
   spec verification). Classification of the 147-paper pool was also
   single-pass; rejected-paper reasons are recorded in the build transcripts.
2. **Bessel-zero mechanism transfer across splits (judgment call, surfaced
   not silently decided).** CDT/dynamical-localization at zeros of J₀ is the
   canonical Floquet mechanism and appears in: B3 train (doublon, J₀ zero
   2.4048), B3 validation (PT coupler 2.4; random dimer 2.405), B4 records.
   Same-system duplicates were forced to one side (both Hubbard-doublon
   records → train), but cross-system mechanism transfer was kept in
   validation on the argument that recognizing the J₀-zero condition in a NEW
   H(t) is precisely the generalization being tested. Flip these to train if
   the owner judges it memorization instead.
3. **2 B3 records `needs_original_paper`** (driven δ-scatterer pair): the knowledge-graph service
   paper metadata mismatched (wrong title) — verify against the original
   publication before hidden/scored use.
4. **Complex quasienergies** (PT-unbroken-broken systems, non-Hermitian
   oscillator) are encoded as separate `*_re` / `*_im` real float fields —
   verifier-compatible by construction.
5. **Family-label hygiene.** Agent-assigned `model_family` slugs needed one
   manual correction round (4 distinct kicked/synthetic systems had been
   lumped as `kicked-ssh`; two doublon-CDT papers had diverging slugs hiding
   a split leak). Family labels should be re-checked whenever records are
   added.
6. **Pool not exhausted.** 44/191 papers had empty the knowledge-graph service graphs (recoverable
   later via graph repair); the `dynamics` (24) and `spectro_response` (14)
   cohorts were excluded by design (heterogeneous outputs); B1 retains ~3
   rejected phase-diagram papers that original-paper access could recover.

## Provenance chain per record

question/answer ← the knowledge-graph service conclusion node (`source_node_id`, verbatim
`source_excerpt`) ← paper graph (`/tmp/asb_scan/graphs/<paper_id>.json`,
fetched 2026-06-12 via the internal knowledge-graph service) ← workflow
#1069 paper list (`data/workflow_1069_paper_ids.txt` from
a sibling benchmark repository).
