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

Consider the four-dimensional Dirac-lattice Floquet model defined by the stroboscopic evolution operator F = exp(-i*H(p)) * exp(-i*V(x)), where H(p) is the 4x4 Dirac Hamiltonian H(p) = K*(mu + sum_{i=1}^{4} cos(p_i)) * Gamma_0 + K*sum_{i=1}^{4} sin(p_i) * Gamma_i with disorder strength parameter 1/K and effective-mass parameter mu, and V(x) = V1(x1) - sum_{i=2}^{4} omega_i * x_i is a separable potential that breaks time-reversal symmetry (V1(x1) = x1^2 * tau_z otimes sigma_0, with tau_z in valley space). The incommensurate driving frequencies omega_i are chosen to be mutually irrational. The model is in symmetry class A (broken time-reversal). At clean-limit (1/K -> 0) the second Chern number satisfies C = -sign(mu) for 2 < |mu| < 4. Scan the effective-mass parameter mu in the range 3.0 to 5.0 at fixed disorder strength 1/K = 1/K_critical to locate the metal-insulator transition between the C=-1 insulating phase and the metallic phase. Use finite-time scaling of the mean-square displacement Delta^2(t) via the anomalous-diffusion scaling form Delta^2(t)/sqrt(t) = D(xi^{-4} * t) with xi ~ |mu - mu_c|^{-nu} to extract the critical mu_c. (The disorder-strength window that produces the metallic phase is approximately 1 < 1/K < 10.) Output a JSON object {"mu_c_classA_C-1": <value>}.
