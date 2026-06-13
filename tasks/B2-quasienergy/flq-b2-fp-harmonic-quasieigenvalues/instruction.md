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

Consider a driven harmonic oscillator with Langevin equation: x_dot = v, v_dot = -gamma*v - omega^2*x + A*sin(omega_0*t + phi) + xi(t), with Gaussian white noise. Parameters: gamma (friction), omega (oscillator frequency), overdamped regime gamma > 2*omega. After introducing a phase variable and applying a periodic coordinate shift, the Fokker-Planck operator separates. Its Floquet quasi-eigenvalue spectrum has the ladder form mu_lmn = i*l*omega_0 + Lambda_mn, where Lambda_mn (non-negative integers m, n; Lambda_00 = 0 is the stationary mode) is built from the two fundamental relaxation rates of the deterministic damped oscillator. Derive closed forms for the two fundamental rates: Lambda_10 (m=1, n=0, the fast rate) and Lambda_01 (m=0, n=1, the slow rate).

Declared symbols:
  gamma  — friction coefficient (>0), overdamped: gamma^2 > 4*omega^2, gamma ∈ [2.5, 5]
  omega  — oscillator frequency (>0), omega ∈ [0.5, 1.2], with gamma^2/4 > omega^2

Output a JSON object {"Lambda_10_formula": "<expr for m=1,n=0>", "Lambda_01_formula": "<expr for m=0,n=1>"} using only the declared symbols and functions [sqrt].
