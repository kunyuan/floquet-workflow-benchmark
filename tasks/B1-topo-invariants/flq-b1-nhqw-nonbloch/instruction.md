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

Consider the non-unitary split-step quantum walk with Floquet (stroboscopic) evolution operator U_0 = T_down * R_y(theta_2) * M * T_up * R_y(theta_1), where R_y(theta) = exp(-i theta sigma_y / 2) is a spin rotation by angle theta about y, M = diag(e^{+gamma}, e^{-gamma}) in the spin basis is a polarization-selective loss with gamma > 0 (so a = e^{gamma} is the loss parameter), and T_up (T_down) are conditional shift operators that translate spin-up right (spin-down left) by one lattice site. The system is defined under open boundary conditions on a 1D lattice. The non-Bloch winding number v is defined by the complex-beta Berry-type integral v = (1/(2*pi)) * sum_{pm} contour_integral_{C_beta^{inside}} d_beta <psi_pm^L(beta)| i * partial_beta |psi_pm^R(beta)>, where |psi_pm^R(beta)> and <psi_pm^L(beta)| are the right and left eigenstates of H_eff(beta) on the generalized Brillouin zone (GBZ), and C_beta^{inside} is the inside branch of the GBZ contour as the boundary parameter Delta -> 0. For parameter values theta_1 = 1.6*pi, theta_2 = 0.58*pi, a = e^{gamma} = 0.82 (i.e., gamma = ln(0.82) ≈ -0.198), which is a topologically nontrivial gapped phase, what is the value of the non-Bloch winding number v? Output a JSON object {"winding_number": <integer>}.
