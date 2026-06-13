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

Consider the periodically driven harmonic oscillator with Hamiltonian H(t) = hbar*omega0*(a_dag*a + 1/2) - hbar*r0*cos(omega_d*t)*(a + a_dag), where omega0 > 0 is the natural frequency, omega_d > 0 is the drive frequency (omega_d != omega0), r0 > 0 is the dimensionless drive amplitude, and a, a_dag are bosonic ladder operators ([a, a_dag] = 1). The exact Floquet quasienergies form a harmonic ladder eps_n (n = 0, 1, 2, ...). The level is fixed at n = 3. Report the dimensionless quasienergy eps_folded = eps_3/omega_d folded into the first Floquet zone (-1/2, 1/2] using the fold() function (fold(x) = x - floor(x + 0.5)).

Declared symbols:
  omega0  — natural frequency (>0), omega0 ∈ [0.8, 1.5]
  omega_d — drive frequency (>0, omega_d ≠ omega0), omega_d ∈ [0.05, 0.4]
  r0      — dimensionless drive amplitude (>0), r0 ∈ [1.0, 3.0]

Output a JSON object {"eps_folded_formula": "<closed-form expression string>"} using only the declared symbols and functions [fold, floor].
