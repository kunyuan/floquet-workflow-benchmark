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

Consider a stack of two-band two-dimensional Chern insulators with a spatially periodic on-site potential V(z) = V_z cos(Q_z z) along the stacking direction z (Q_z = 2pi/lambda_z). The static layer Hamiltonian density is H(k_x, k_y, z) = [m_z + V_z cos(Q_z z)] sigma_z + m_0 [2 - cos(k_x a) - cos(k_y a)] sigma_z + t_x sin(k_x a) sigma_x + t_y sin(k_y a) sigma_y, with parameters m_z = 0.5 eV, m_0 = 1 eV, V_z = 1 eV, t_x = t_y = t_0 = 1 eV, a = 1 nm, and modulation period lambda_z = 31a. A linearly polarized time-periodic electric field of frequency omega and amplitude E_0 is additionally applied (dimensionless drive amplitude A_0 = e E_0 / (hbar omega), units nm^{-1}). In the high-frequency Floquet limit, the electric field renormalizes the effective layer mass. Floquet Weyl-like nodes (gap closings at k_x = k_y = 0) exist for small A_0; as A_0 increases the two nodes approach each other. Scan A_0 from 0 to 1.5 nm^{-1}. Locate the critical drive amplitude A_0_c at which the two Floquet Weyl-like nodes coalesce and annihilate — the transition from the Weyl-like phase to a fully gapped phase — identified by the merging of the two gap-closing momenta along the stacking direction into a single point and the simultaneous opening of a gap. Report the result to four significant figures. Output a JSON object {"A0c_inv_nm": <value>}.
