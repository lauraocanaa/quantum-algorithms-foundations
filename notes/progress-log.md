# Progress Log

Personal log of study and implementation work undertaken in preparation for graduate
applications in computational physics — spanning quantum computing, scientific
computing, and computational nuclear physics. For the polished project overview and
validated results, see the main [README](../README.md).

## Week 1

- **Environment:** local Qiskit setup (Python 3.13, Qiskit 2.4.1, Qiskit-Aer, Jupyter), verified with a test circuit
- **Theory:** Nielsen & Chuang, Ch. 1, §1.2–1.4.3 (qubits, gates, circuits, introduction to Deutsch's algorithm)
- **Mathematics:** Hadamard eigenstructure (λ = ±1), tensor product structure (H⊗H vs H⊗I acting on |00⟩)
- **IBM Quantum Learning:** completed Modules 1, 2, 3, 4, 5, and 8 — Single Systems, Multiple Systems, Quantum Circuits, Entanglement in Action, Quantum Query Algorithms, and Grover's Algorithm

**Known issue:** Qiskit-Aer has a reported import hang on Windows + Python 3.13 on first
run; resolves on its own and is not a broken install. `StatevectorSampler` works as a
fallback backend.

## Week 2

- **Implemented:** Bell state circuit and verification — measured counts `{'00': 506, '11': 494}` (1000 shots), 0% leakage into `|01⟩`/`|10⟩` — consistent with the ideal Bell state within statistical noise
- **Implemented:** Deutsch's algorithm, all four oracle cases (`f0`, `f1`, `fx`, `f1x`) — single-qubit circuit with an ancilla prepared in `|1⟩` and Hadamard'd for phase kickback; the constant cases apply no gate (`f0`) or a single X on the ancilla (`f1`); the balanced cases apply a CNOT (`fx`, identity-balanced) or a CNOT conjugated by X gates on the control (`f1x`, NOT-balanced). All four verified against expected classification via 1000-shot measurement of the control qubit.

## Week 3

- **Implemented:** n-qubit Deutsch–Jozsa, verified at n = 2, 3, 4 — generalized the oracle construction as functions of n: the constant-0 oracle applies no gates, the constant-1 oracle applies a single X to the ancilla, and the balanced oracle applies a CNOT from every input qubit to the ancilla (n-bit parity function). The main DJ circuit required no modification across qubit counts. All three oracle types were correctly classified with 100% measurement consistency (1024/1024 shots) at every tested n.
- **Implemented:** 2-qubit Grover's algorithm — built a phase oracle marking a target bitstring via X gates conjugating a controlled-Z (flipping 0-bits before/after the CZ so the phase flip lands only on the marked state), and a diffusion operator (H⊗H, reflection about `|00⟩` reusing the oracle construction, H⊗H). Marked `|11⟩` with 1 iteration — the theoretically optimal k for N=4, M=1. Measured 100% success (1024/1024 shots), matching the exact-resonance prediction for this configuration.
- **Implemented:** 3-qubit Grover's algorithm — generalized the oracle and diffusion operator to 3 qubits using a multi-controlled Z built from H + CCX + H on the target qubit (the 3-qubit analogue of the 2-qubit CZ), with the same conjugate-flip structure to mark an arbitrary target state. Marked `|101⟩` with k=2 iterations, chosen via k = round((π/4)√8 − 0.5) for N=8, M=1. Measured 94.04% success vs a theoretical 94.5% — illustrating the near-resonance case, where the optimal integer iteration count doesn't land exactly on the amplitude peak (unlike the 2-qubit case above, which hits exact resonance).

## Week 4

- **Implemented:** Infinite square well solved via finite-difference discretization (tridiagonal Hamiltonian, natural units ħ=m=L=1). Validated against analytic eigenvalues E_n = n²π²/2. Convergence rate measured at 1.998 (theoretical prediction: 2.0), confirming O(h²) accuracy of the central difference scheme.
Eigenvector validation complete: numerical eigenvectors (N=500) match analytic ψₙ(x)=√(2/L)sin(nπx/L) for n=1,2,3 to visual precision. Eigenvalue errors: 1.62e-05 (n=1), 2.59e-04 (n=2), 1.31e-03 (n=3), consistent with expected growth in finite-difference error at higher curvature. Debugged a stale-N grid-spacing mismatch causing a ~π factor amplitude error — dx must be derived from the same N used to build H.

