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

Consider the extended Benalcazar-Bernevig-Hughes (BBH) square-lattice model with momentum-space Hamiltonian H(k) = d(k) . Gamma, where Gamma_1 = tau_y sigma_1, Gamma_2 = tau_y sigma_2, Gamma_3 = tau_y sigma_3, Gamma_4 = tau_z sigma_0, Gamma_5 = tau_x sigma_0 (tau and sigma are Pauli matrices for two sets of degrees of freedom), and the five d-components are: d_1(k) = -(lambda*sin(k_y) + m*sin(2*k_x)), d_2(k) = -(gamma_0 + lambda*cos(k_y) + m*cos(2*k_x)), d_3(k) = -(lambda*sin(k_x) + m*sin(2*k_y)), d_4(k) = 0, d_5(k) = gamma_0 + lambda*cos(k_x) + m*cos(2*k_y), where gamma_0 is the intracell hopping, lambda is the intercell hopping, and m is the long-range hopping amplitude. Apply a two-step periodic drive modulating the long-range hopping as m(t) = m_1 for t in [n*T, n*T + T_1) and m(t) = m_2 for t in [n*T + T_1, (n+1)*T), giving one-period evolution U_T(k) = exp(-i*H_2(k)*T_2)*exp(-i*H_1(k)*T_1), with H_l(k) evaluated at m = m_l. Use parameter values: lambda = 0.64*gamma_0, m_1 = -0.36*gamma_0, m_2 = 3.6*gamma_0, T_1 = 1.2/gamma_0, T_2 = 0.6/gamma_0 (total period T = T_1 + T_2 = 1.8/gamma_0). From the dressed effective Hamiltonians H_{eff,l}(k) = i/T * ln[F_l(k) * U_T(k) * F_l^dagger(k)] where F_l(k) = exp(i*(-1)^l * H_l(k)*T_l/2), compute the Floquet second-order topological indices N_0 and N_pi (dressed chiral numbers in the 0 and pi quasienergy gaps) and the real Chern number V_R. Also count corner_states_pi_gap, defined as the total number of pi-gap corner-localized Floquet modes on the open square sample (modes whose quasienergy is at or near |pi/T| and whose weight is concentrated at the corners of the square lattice). Output a JSON object {"N_0": <integer>, "N_pi": <integer>, "V_R": <integer>, "corner_states_pi_gap": <integer>}.
