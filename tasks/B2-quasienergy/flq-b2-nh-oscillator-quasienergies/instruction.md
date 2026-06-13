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

Consider the non-Hermitian driven harmonic oscillator with Hamiltonian (hbar = 1) H = (omega - i*gamma)*(a_dag*a + 1/2) + f0*cos(Omega_d*t)*(a + a_dag), where omega > 0 is the natural frequency, gamma > 0 is the damping rate, f0 > 0 is the real drive amplitude, and Omega_d > 0 is the drive frequency. The Floquet quasienergies form a complex ladder eps_n (n = 0, 1, 2, ...) with Im(eps_n) < 0 signaling exponential decay. Derive the closed-form complex expressions for eps_0/omega and eps_1/omega.

Declared symbols:
  omega   — natural frequency (>0), omega ∈ [0.8, 2.0]
  gamma   — damping rate (>0), gamma ∈ [0.05, 0.5]
  Omega_d — drive frequency (>0), Omega_d ∈ [0.2, 1.0]
  f0      — real drive amplitude (>0), f0 ∈ [0.2, 1.5]

Output a JSON object {"eps0_over_omega": "<complex expression>", "eps1_over_omega": "<complex expression>"} using only the declared symbols and literal 1j for the imaginary unit.
