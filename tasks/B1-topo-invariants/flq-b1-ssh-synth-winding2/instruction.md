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

Consider a synthetic-frequency-dimension dimer chain realized in a fiber-loop cavity with two electro-optic modulators (EOMs). The effective Hamiltonian is H(k) = [[0, g(k)], [g*(k), 0]] where the off-diagonal function is g(k) = i*eta*[V_a + V_b*exp(i*k*Omega) - V_c*exp(-i*k*Omega) - V_d*exp(2*i*k*Omega)], with k the crystal momentum along the synthetic frequency dimension and Omega the free spectral range. The hopping coefficients are a = i*eta*V_a, b = i*eta*V_b, c = -i*eta*V_c, d = -i*eta*V_d. The constraint a = b* is enforced, all magnitudes are real-valued ratios, and the complex phase of d is theta = arg(d). The hopping magnitudes are fixed at |c|/|a| = 0.854 (c real and negative) and |d|/|a| = 2.27, with a = b* real. Starting from initial phase arg(d) = 0 (which places the system in the W = 2 phase), the phase theta = arg(d) is continuously tuned to arg(d) = pi, passing through a gap-closing topological transition near arg(d) = pi/2. (Note: this model has third-neighbor reach, so |W| <= 2.) What is the winding number W in the final phase at arg(d) = pi? Output a JSON object {"winding_number": <integer>}.
