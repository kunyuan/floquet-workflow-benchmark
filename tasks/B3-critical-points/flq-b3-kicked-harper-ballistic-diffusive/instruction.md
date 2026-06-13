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

Consider the one-dimensional kicked Harper model (KHM) with Hamiltonian H_KHM = 2J*cos(2*pi*Q*n) + 2J*cos(p/hbar), where n is the site index, p is the conjugate momentum, Q=(sqrt(5)-1)/2 is the incommensurate spatial frequency, hopping amplitude J=1, and hbar=1/8. The unperturbed on-site potential strength is V=0.2, placing the system in the extended (ballistic) regime with unperturbed MSD scaling as m2(t) ~ t^2. A polychromatic harmonic perturbation f_epsilon(t) = (epsilon/sqrt(M)) * sum_{i=1}^{M} cos(omega_i * t) is added, with M=3 mutually incommensurate frequencies omega_i of order 1. At each time step, apply the kick H_kick = 2V*cos(2*pi*Q*n) + f_epsilon(t) to the state, alternating with the kinetic propagator exp(-i*2*cos(p/hbar)*dt/hbar). Compute the long-time mean-square displacement m2(t) = sum_n (n - N/2)^2 * |phi(n,t)|^2 starting from phi(n,0) = delta_{n,N/2}. Scan the perturbation amplitude epsilon from 0 to 0.5. Locate the critical amplitude epsilon_b at which the long-time asymptotic behavior transitions from ballistic scaling (m2 ~ t^2) to normal diffusion (m2 ~ t^1), identified by the crossover in the long-time exponent alpha where m2(t) ~ t^alpha. Output a JSON object {"epsilon_b": <value>}.
