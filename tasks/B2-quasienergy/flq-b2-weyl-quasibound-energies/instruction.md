# Workflow context (common to every task in this suite)

You are solving an instance of the **Floquet effective Hamiltonian derivation
and analysis** workflow. Problems of this class are solved by the following
pipeline:

1. **Define the time-periodic Hamiltonian** — specify the system and driving
   parameters to obtain H(t) with period T = 2π/ω.
2. **Choose a Floquet approach** — select the appropriate method (exact
   diagonalization of the Floquet matrix, one-period evolution operator,
   high-frequency expansion, degenerate perturbation theory) based on the
   driving frequency and amplitude regime.
3. **Construct the effective Floquet Hamiltonian or Floquet matrix** — obtain
   a time-independent representation generating the stroboscopic dynamics.
4. **Compute quasienergies and Floquet states** — obtain the quasienergy
   spectrum and the corresponding Floquet states.
5. **Evaluate observables and dynamics** — use the Floquet states to compute
   the requested time-averaged or stroboscopic quantities (gaps, invariants,
   critical parameters, effective couplings, …).

Sanity-check your results against exact numerical Floquet evolution for small
systems where feasible, and check convergence with truncation and time-step
parameters.

The task below is one concrete problem from this family. Apply the workflow;
the specific system, parameters, conventions, and requested outputs follow.

---

# Environment & answer protocol (common to every task in this suite)

- Compute environment: Python 3 with numpy and scipy available. No internet
  access is required or assumed; everything needed is stated in the task.
- Work in the task directory. You may write any scratch files you need.
- **Answer emission**: write your final answer to `pred.json` in the task
  directory — a single JSON object whose keys are exactly the quantity ids
  requested in the task text (no extra keys). Numeric values as JSON numbers;
  formula-type answers as expression strings using only the symbols the task
  declares.
- Report numeric values to at least 6 significant digits unless the task
  states a different precision.
- Convergence is your responsibility: where a calculation involves
  truncation, grid, or time-step choices, converge them until your answer is
  stable at the reported precision.
- **Derivation log (required)**: alongside `pred.json`, write
  `derivation.md` — a detailed step-by-step account of your solution,
  organized by the workflow steps above (1. model setup → 2. method choice
  and why → 3. construction → 4. spectrum → 5. observables). Show the
  actual derivation: intermediate expressions, the equations you solved,
  numerical convergence checks, and how each requested quantity was
  obtained. State explicitly where you made approximations and why they are
  valid in this regime. This log is not scored against the gold but is
  collected with your answer.

---

Consider a three-dimensional tilted Weyl semimetal (hbar=1) with a one-dimensional square-well potential V(x) = -V_0 for |x| <= L/2, V(x) = 0 for |x| > L/2 applied along the x direction. Conserved momenta ky and kz label the transverse plane-wave factors. For l=0 (ground quasi-bound level), the quantized longitudinal wavenumber is q_0 = pi/(2*L). The chirality is s=+1. Energy reference: all energies are measured relative to V=0 outside the well (inside the well V(x) = -V0 with V0 > 0). The quasi-bound Fano resonance states lie above the continuum edge, so E_b > 0 for all valid parameter choices.

The tilt parameter is t_tilde = 2*t1*sin(phi1 - k0) + 4*t2*sin(phi2 - 2*k0). Derive the closed-form energies E_b of the two quasi-bound branches (the plus/minus pair) of the l=0 level, accounting for the well shift, the anisotropic Weyl dispersion (transverse velocity t in the x and y directions, z-direction velocity tz*sin(k0)), and the tilt contribution along z.

Declared symbols:
  V0     — well depth (>0), V0 ∈ [3, 8]
  t      — transverse Weyl velocity (>0), t ∈ [0.5, 2]
  kz     — conserved z-momentum, kz ∈ [0.5, 2]
  ky     — conserved y-momentum, ky ∈ [0.2, 1]
  k0     — Weyl node wavenumber, k0 ∈ [0.5, 2.5]
  t1     — first tilt coefficient, t1 ∈ [0, 0.5]
  t2     — second tilt coefficient, t2 ∈ [0, 0.15]
  L_lat  — well half-length L, L_lat ∈ [0.5, 2]
  tz     — z-direction Weyl velocity, tz ∈ [0.5, 2]
  phi1   — tilt phase offset 1, phi1 ∈ [0, 0.5]
  phi2   — tilt phase offset 2, phi2 ∈ [0, 0.5]

Output a JSON object {"Eb_plus_formula": "<expr>", "Eb_minus_formula": "<expr>"} using only the declared symbols and functions [sqrt, sin, pi].
