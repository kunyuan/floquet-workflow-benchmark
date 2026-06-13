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

Consider a 1D cold-atom Raman lattice with Zeeman splitting m_z, spin-conserved hopping amplitude v_0, and spin-orbit coupling amplitude v_so. In the static regime the system is trivial when |m_z| > 2|v_0|. Apply a periodic quenching protocol that switches the spin-orbit coupling phase between 0 and pi (equivalently, v_so -> -v_so) with driving period T. The gap-closing conditions occur when T*|m_z - 2*v_0*exp(i*alpha)| = n_alpha * pi for odd integers n_alpha and alpha in {0, pi} (where alpha = 0 corresponds to k = 0 and alpha = pi corresponds to k = pi). The winding number W changes by +1 (decreases by 1) at each gap-closing associated with alpha = 0 (alpha = pi) as T increases. Starting from W = 0 at small T, and using parameter values m_z = 3*v_0 and v_so = v_0, determine the winding number W in the Floquet phase with the largest |W| that is reachable by increasing T continuously from zero while remaining in a gapped phase. This is the winding number of the 6th distinct topological phase encountered as T increases. Output a JSON object {"winding_number": <integer>}.
