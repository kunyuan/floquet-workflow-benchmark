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

Consider a 2D topological insulator on a square lattice with nearest-neighbor hopping t_x = t_y = 1.0, spin-orbit coupling lambda_x = lambda_y = 1.0, crystal-field splitting m_0 = 2.5, and proximity-induced d-wave superconducting pairing Delta = 0.6 (pairing function Delta(k) = Delta*(cos(k_x) - cos(k_y))). The static Hamiltonian H_0(k) is in the trivial phase since |m_0| = 2.5 > t_x + t_y = 2.0. A periodic mass kick is applied: the mass term (proportional to Gamma_1 = sigma_z * tau_z, where sigma and tau are Pauli matrices for spin and particle-hole degrees of freedom) is kicked as m(t) = m_1 * sum_r delta(t - r*T) with amplitude m_1 = -0.4 and period T = 0.419. No in-plane Zeeman field is applied (B_x = 0). The one-period Floquet evolution operator is U(T) = exp(-i*m_1*Gamma_1) * exp(-i*H_0(k)*T). Under open boundary conditions on a square sample, this driving generates a Floquet second-order topological superconducting (FSOTSC) phase. How many zero-energy Majorana corner modes (MCMs) appear in total at the four corners of the square sample? Output a JSON object {"majorana_corner_modes_total": <integer>}.
