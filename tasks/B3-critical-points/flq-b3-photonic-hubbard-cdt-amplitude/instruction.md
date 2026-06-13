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

Consider a two-dimensional square photonic waveguide lattice acting as a simulator of the one-dimensional two-particle Hubbard model. The propagation coordinate z plays the role of time. The Floquet Hamiltonian is H(z) = sum_{l,m} [Delta_beta * delta_{l,m on diagonal}] |l,m><l,m| + kappa * sum_{<i,j>} (|i><j| + h.c.) + A * sum_{l,m on diagonal} cos(omega * z) |l,m><l,m|, where kappa = 0.04 mm^{-1} is the nearest-neighbor coupling, Delta_beta = -0.18 mm^{-1} is the fixed diagonal on-site shift, omega = 1.57 mm^{-1} is the spatial modulation frequency, and A (in micrometers of physical waveguide displacement, with an effective coupling determined by the modulation geometry) is the sinusoidal modulation amplitude applied to diagonal (doublon-carrying) waveguides. The one-period Floquet evolution operator is U = T-exp[-i integral_0^{z_0} H(z') dz'] where z_0 = 2*pi/omega. In the two-particle sector, the Floquet quasienergy spectrum splits into a narrow paired (doublon) miniband and a wider unpaired band. Scan A from 1 to 15 micrometers. Report the critical amplitude A_CDT (in micrometers) at which coherent destruction of tunneling (CDT) of the paired state occurs — identified as the drive amplitude that produces maximum localization (highest inverse participation ratio, IPR) of the doublon at the lattice output and at which the paired Floquet miniband undergoes an approximate collapse. Output a JSON object {"A_CDT_um": <value>}.
