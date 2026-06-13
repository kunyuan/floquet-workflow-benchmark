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

A spatially-homogeneous photonic temporal crystal has a square-wave relative permittivity: epsilon(t) = epsilon_1 for 0 < t < T_1, and epsilon(t) = epsilon_2 for T_1 < t < T_2 (T_2=T-T_1), with period T and speed of light c. For wavenumber k, define the phase advances in the two half-periods phi1 = k*c*T_1/sqrt(epsilon_1) and phi2 = k*c*T_2/sqrt(epsilon_2), and the impedance ratio r_imp = sqrt(epsilon_2/epsilon_1). Work in the elliptic (stable band) regime, where the magnitude of the one-period monodromy trace is below 2. Using the transfer-matrix (monodromy) method for piecewise-constant media, derive the dimensionless quasi-frequency phase per period Omega_k*T of the Floquet (Bloch-in-time) modes, taking the principal value in [0, pi].

Declared symbols:
  phi1  — phase advance in medium 1, phi1 ∈ (0, 1.0] rad
  phi2  — phase advance in medium 2, phi2 ∈ (0, 0.6] rad
  r_imp — impedance ratio sqrt(epsilon_2/epsilon_1), r_imp ∈ [1.2, 3.5]

Output a JSON object {"Omega_k_T_formula": "<closed-form expression string>"} using only the declared symbols and the functions [cos, sin, arccos, sqrt].
