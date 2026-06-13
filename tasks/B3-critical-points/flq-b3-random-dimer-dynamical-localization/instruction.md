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

Consider a one-dimensional random-dimer tight-binding chain with N=1501 sites, nearest-neighbor hopping amplitude R=1, and a dimer detuning epsilon_minus = |epsilon_b - epsilon_a| = R/3. The dimers are distributed randomly along the chain (dimer concentration Q=0.5). An AC electric field E(t) = E1 * cos(omega*t) is applied, giving a gauge-transformed hopping phase exp(i*beta*sin(omega*t)) where beta = e*d*E1/omega (e is carrier charge, d is lattice spacing). Work in the high-frequency regime R/omega = 0.3. Run the full Floquet pipeline at each beta: compute the one-period evolution operator for the driven chain, diagonalize to obtain Floquet states, and compute the mean-square displacement MSD(t) for an initially localized wavepacket C_n(0) = delta_{n,0}. Scan the drive parameter beta from 0 to 4. Locate the FIRST critical value beta_DL at which dynamical localization of the entire chain sets in — that is, the first drive amplitude at which the quasienergy bandwidth collapses and MSD(t) remains bounded for all long times. Output a JSON object {"beta_DL_first": <value>}.
