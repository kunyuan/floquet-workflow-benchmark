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

Consider a one-dimensional Floquet topological circuit for digital quantum simulation of spin-orbit coupled lattice physics. A spinful lattice of N sites is encoded in 2N qubits: odd qubit Q_{2x-1} encodes spin-up and even qubit Q_{2x} encodes spin-down at site x. The one-period Floquet evolution operator is U_1 = [tensor over x: U(alpha/2) on (Q_{2x-1},Q_{2x})] * [tensor over x: U(beta) on (Q_{2x},Q_{2x+1})] * [tensor over x: U(alpha/2) on (Q_{2x-1},Q_{2x})], where U(theta) is a composite two-qubit gate implementing SOC hopping via U(theta) = CNOT_{Q_a,Q_b} Z^+_{Q_a} Y^-_{Q_a}(theta) CNOT_{Q_b,Q_a} Y^+_{Q_a}(theta) CNOT_{Q_b,Q_a} Z^-_{Q_a} CNOT_{Q_a,Q_b}, with Y^pm(theta) = exp(mp*i*(theta/2)*sigma_y), Z^pm = exp(mp*i*(3*pi/4)*sigma_z), acting in the single-excitation subspace. The topological invariants (nu_0, nu_pi) are defined as the integer winding numbers nu_epsilon = (i/(4*pi)) * integral_{-pi}^{pi} dk tr(tau_z * U_{1,epsilon}^{-1} * d/dk U_{1,epsilon}) for epsilon in {0, pi}, where U_{1,epsilon}(k) is the periodized Floquet operator in the two-component internal basis and tau_z is the corresponding Pauli z matrix. For circuit parameters alpha = pi and beta = 3*pi/2 (with alpha, beta in (0, 2*pi)), what are the Floquet winding numbers nu_0 and nu_pi? Output a JSON object {"nu_0": <integer>, "nu_pi": <integer>}.
