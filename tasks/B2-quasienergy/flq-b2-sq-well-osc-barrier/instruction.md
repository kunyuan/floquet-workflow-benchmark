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

Consider the one-dimensional quantum particle with time-periodic potential V(x,t) = ∞ for x<0; 0 for 0≤x<a; V₀+V₁cos(ωt) for a≤x≤b; V₀' for x>b, with all lengths and energies in atomic units (ℏ=m_e=e=1). Parameters: a=1 a.u., b=2 a.u., V₀=15 a.u., V₀'=V₀/2=7.5 a.u., V₁=0.2·V₀=3 a.u., drive frequency ω=0.62·V₀=9.3 a.u. Using a two-sideband (N=2) Floquet secular-equation truncation, two metastable Floquet states exist. Report their Floquet quasienergies as DIMENSIONLESS values ε/ω, where the real part is folded into the first Floquet zone (-1/2, 1/2]. Include the imaginary part (Im ε/ω < 0 signals decay). Label them by their relative stability: 'eps_less_stable' for the state with larger |Im ε| (faster decay) and 'eps_more_stable' for the state with smaller |Im ε|. Output a JSON object {"eps_less_stable_re": <float>, "eps_less_stable_im": <float>, "eps_more_stable_re": <float>, "eps_more_stable_im": <float>}.
