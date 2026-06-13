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

Consider a one-dimensional PXP chain of L qubits (L even, L divisible by 3, periodic boundary conditions) with the stroboscopic Floquet unitary U_{τ}=exp(-iτH_e)exp(-iτH_o), where H_e=Σ_{j even} P_{j-1}X_j P_{j+1} and H_o=Σ_{j odd} P_{j-1}X_j P_{j+1}, P_j=|0⟩_j⟨0|, X_j=|0⟩_j⟨1|+|1⟩_j⟨0|, evaluated at the integrable Trotter step τ=π/2. At this step the dynamics is equivalent to a classical cellular automaton (CA). The three translationally symmetric CA-vacuum eigenstates of U_{π/2} are constructed from the classical period-3 product configurations |0⟩^⊗L, |01⟩^⊗(L/2), |10⟩^⊗(L/2). The three vacuum quasienergies are folded dimensionless values ε/ω_eff (ω_eff=2π), determined by the CA eigenvalue condition ε₀∈{0,±2π/3} rad.

Output a JSON object {"eps_vacuum_0_formula": "<expr>", "eps_vacuum_plus_formula": "<expr>", "eps_vacuum_minus_formula": "<expr>"} using only Python arithmetic and the constants pi. Expressions are constant (no free variables needed).
