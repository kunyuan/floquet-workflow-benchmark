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

Consider the kicked extended SSH model: a one-dimensional chain with momentum-space Hamiltonian H(k) = d_x(k)*sigma_x + d_y(k)*sigma_y + d_z(k)*sigma_z, where d_x(k) = t*(1 + delta*cos(theta)) + t*(1 - delta*cos(theta))*cos(k), d_y(k) = t*(1 - delta*cos(theta))*sin(k), d_z(k) = g + h*cos(theta - phi). Here theta is a synthetic (crystal-angle) parameter, phi is an offset, t is the hopping amplitude, delta parameterizes the dimerization, g and h are on-site potential parameters. The system is periodically kicked in the y-direction: H_kick = alpha_y * sigma_y * sum_m delta(t - m*T), so the one-period Floquet evolution operator is U(k, theta) = exp(-i*alpha_y*sigma_y) * exp(-i*H(k, theta)*T). Using parameters t = 1, delta = 0.5, h = 1, T = 3, alpha_y = 0.8 (with alpha_x = alpha_z = 0), and treating (k, theta) as a 2D synthetic Brillouin zone and scanning over the full two-parameter space (g, phi) to find the phase with maximum |C| (note: at phi=0 a theta -> -theta symmetry forces C=0, so phi != 0 is required): what is the maximum magnitude of the stroboscopic Chern number C achievable by this Y-kicking protocol? Output a JSON object {"max_chern_number_magnitude": <integer>}.
