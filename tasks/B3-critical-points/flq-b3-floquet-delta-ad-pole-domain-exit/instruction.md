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

Consider the one-dimensional delta-function scatterer with time-periodic potential H(x,t) = -(hbar^2 / 2mu) d^2/dx^2 + [V_s + V_d cos(omega t)] delta(x), with static potential V_s = 0 (no static component). Define the dimensionless driving strength a_d = mu V_d^2 / (8 hbar^3 omega) and scaled kinetic energy epsilon = E / (hbar omega). Quasibound-state energies epsilon = epsilon_R - i epsilon_I (epsilon_I > 0) are found by solving the infinite tridiagonal outgoing-wave matrix equation with diagonal entries sqrt(epsilon + n) (a_s = 0) and nearest-neighbor off-diagonals i sqrt(a_d). The 'domain D_0' is defined by 0 < epsilon_R < 1 (between photon-sideband thresholds at epsilon_R = 0 and epsilon_R = 1). A quasibound pole exists in D_0 for small a_d > 0. Scan a_d from 0 to 1.5. After the transmission zero disappears at the first critical driving strength, the corresponding quasibound pole continues to move; locate the second critical value a_d_c2 at which the pole's real part crosses the lower photon-sideband threshold at epsilon_R = 0, causing the pole to exit D_0. Report the result to three significant figures. Output a JSON object {"a_d_c2": <value>}.
