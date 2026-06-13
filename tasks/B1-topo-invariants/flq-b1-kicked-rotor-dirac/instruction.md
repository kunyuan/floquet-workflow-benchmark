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

Consider a quantum resonance (N=3) of a periodically kicked rigid rotor (linear diatomic molecule) with rotational constant B, driven at quantum-resonance period T = tau_B/3 where tau_B = h/B is the rotational revival time. The kick Hamiltonian consists of two terms: H_kick = sum_q [P_1(alpha)*cos^2(theta_hat) + P_2(alpha)*cos(theta_hat)] * delta(t - q*T), where P_1(alpha) = P*cos^2(alpha), P_2(alpha) = P*sin^2(alpha), with overall kick strength P = 2.5 (in dimensionless units where B = 1) and offset parameter alpha in [0, 2*pi). In the angular-momentum lattice representation, the Floquet operator after one period maps angular momentum states |l> -> |l> and has an effective Bloch Hamiltonian H(k, alpha) that is a 3x3 matrix (N=3 periodicity) with two Dirac cones where the second and third Floquet bands touch at k = pi. Treating (k, alpha) as a 2D synthetic Brillouin zone, the Berry phase accumulated around a small closed loop encircling each cone is quantized. How many topological edge states are present at the boundary of a half-infinite angular-momentum lattice (l >= 0), connecting the two Dirac cones across the Brillouin zone? Output a JSON object {"edge_state_count": <integer>}.
