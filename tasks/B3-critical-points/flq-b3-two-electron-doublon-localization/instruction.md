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

Consider a one-dimensional tight-binding lattice with N sites, single-electron transfer integral Delta=1, and on-site Hubbard repulsion U=10 (large-U regime, U >> Delta). Both electrons start colocated at site 0: C_{l,m}(0) = delta_{l,0}*delta_{m,0}. A spatially uniform oscillating electric field is applied such that the single-electron coupling is -eE(t)*d = A*cos(omega*t) with drive frequency omega=1 and variable amplitude A. The doublon (on-site two-electron bound state) carries charge -2e and thus couples to the field as -2eE(t)*d = 2A*cos(omega*t) for its center-of-mass coordinate. Run the full Floquet pipeline: for each A value compute the one-period evolution operator U(T,0) (T=2*pi/omega) of the two-electron Hamiltonian, diagonalize it to obtain Floquet quasienergies, and identify Floquet states with doublon character (same-site weight > 0.9). The dynamic localization condition for the doublon is reached when the doublon quasienergy band collapses — that is, the first drive amplitude at which coherent spreading of the doublon is suppressed and the bandwidth of the doublon Floquet miniband goes to zero. Scan A/omega from 0.5 to 2.0. Report the first critical amplitude ratio (A/omega)_DL at which the doublon band collapses. Units: A and omega share the same energy units (hbar=1). Output a JSON object {"A_over_omega_DL": <value>}.
