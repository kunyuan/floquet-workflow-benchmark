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

Consider a graphene antidot lattice with supercell lattice constant L=3.0 nm and circular holes of diameter D=1.6 nm, irradiated by a monochromatic circularly polarized laser with photon energy hbar*Omega=0.8 eV and spatially uniform electric-field amplitude E0 (in atomic units). The static electronic bandstructure of the antidot lattice is computed non-perturbatively using a Dirac-equation plane-wave expansion in the antidot supercell, and the resulting Bloch states serve as the basis for constructing the Floquet Hamiltonian. The Floquet quasienergy spectrum is obtained by diagonalizing the full Floquet Hamiltonian matrix (including all photon-dressed sidebands up to convergence) at each crystal momentum k. Define the quasienergy gap at the Brillouin-zone center (Gamma point) as Delta_epsilon(Gamma) = epsilon_c,Gamma - epsilon_v,Gamma, where epsilon_c and epsilon_v are the lowest conduction and highest valence quasienergy bands. Scan E0 from 0 to 5 a.u. and locate the FIRST critical driving amplitude E0c1 at which Delta_epsilon(Gamma) closes (goes to zero), signaling a Floquet Dirac-point restoration at Gamma. This transition is identified by the appearance of a linear (Dirac-like) quasienergy dispersion near Gamma. Report the critical electric-field amplitude in atomic units. Output a JSON object {"E0c1_au": <value>}.
