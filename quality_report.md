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

### Gold disputes — ADJUDICATED against the knowledge-graph service + the original papers (2026-06-13)

The baseline run surfaced these; each was then cross-checked against the the knowledge-graph service
node AND the original publication. Outcome: **1 genuine gold error (an the knowledge-graph service
fabrication), 5 question defects with correct golds, 1 gold still unreliable.**

| record | verdict | action taken |
|---|---|---|
| `tbg-circpol-W-spectral` | **GOLD ERROR**: the "spectral winding W=−1" does **not appear in the paper** (arXiv:1910.13510) — an the knowledge-graph service formalization fabricated the invariant. | gold REPLACED with the paper's actual Fig.5 result: lower Floquet band Chern number C=−1 at K valley under σ+; question rewritten. → `paper_verified` |
| `bbh-n0-0-npi-4` | gold CORRECT (arXiv:2504.14846 states N_0=0, N_π=4, V_R=1, 16 corner states); solver erred (used the untwisted chiral operator; counted per-corner not total). | V_R **dropped** (its correct value needs the paper's PT-class-conversion punchline — can't be stated in Q without leaking); corner count clarified as total over 4 corners. → `paper_verified` |
| `kicked-ssh-chern2` | gold CORRECT (DOI 10.1007/s10773-020-04545-7: Y-kick gives C=±2); question forced φ=0 where a θ→−θ symmetry pins C=0. | question fixed to a 2D (g,φ) scan with φ≠0. → `paper_verified` |
| `graphene-floquet-freq` | gold CORRECT (Eq.24); solver's extra vF^4 came from a different λ convention. | question now defines λ=(e·vF/c)·A₀. → `paper_verified` |
| `ssh-synth-winding2` | gold CORRECT (arXiv:2307.01283, W=1 verified); question lacked hopping magnitudes. | magnitudes |c|/|a|=0.854, |d|/|a|=2.27, arg(d):0→π added. → `paper_verified` |
| `4d-qhe-muc-classA` | gold CORRECT (Table II, μ_c=3.51) but the value is a scaling fixed-point read off the Fig.1 phase boundary — **not cleanly self-contained**. | kept `needs_original_paper` with the finding documented. |
| `dqs-floquet-1d-nu0-nupi` | **GOLD UNRELIABLE**: α=π,β=3π/2 sits on a phase boundary (π-gap closed) → ν_π undefined; gold (1,1) is a gapless-point artifact, not a valid bulk phase (off-boundary: (1,2) or (1,0)). the knowledge-graph service graph empty. | **RECORD REMOVED** from the suite (no reliable gold; not worth carrying a do-not-score stub). |

Methodological payoff: QA-6's formula-faithful recompute "confirmed" several
of these from the source formula, yet independent re-derivation from H(t)
(the baseline run) disagreed — because QA-6 cannot catch a wrong *premise*,
only an independent model build can. The single clearest catch is the **the knowledge-graph service
fabrication** in `tbg`: a formalization invented an invariant absent from the
paper. This is the strongest argument for the baseline-run-as-QA layer.

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

40 records / 4 tracks (B1 11, B2 12, B3 10, B4 7; dqs removed post-adjudication), all materialized as harbor
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

## Final inventory: 40 records (after removing dqs in adjudication)

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
