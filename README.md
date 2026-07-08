# Quantum Algorithms: Foundations

Implementation and empirical validation of foundational quantum algorithms, built as
groundwork for hybrid quantum-classical methods (variational algorithms, quantum
simulation). Part of a broader portfolio in computational physics and applied
mathematics — see [profile README] for the full set of projects spanning quantum
computing, numerical PDE methods, and computational nuclear physics.

## Overview
| # | Algorithm | Concept demonstrated | Qubits | Validation |
|---|-----------|----------------------|--------|------------|
| 01 | Bell state | Entanglement, superposition | 2 | 50.6% \|00⟩ / 49.4% \|11⟩, 0% leakage into \|01⟩/\|10⟩ (1000 shots) — consistent with ideal Bell state within statistical noise |
| 02 | Deutsch's algorithm | Query complexity separation, oracle design | 1 | All 4 oracle cases verified against expected output |
| 03 | Deutsch–Jozsa (n-qubit) | Generalised oracle, exponential classical/quantum query gap | n = 3 | Constant (f=0, f=1) and balanced oracles all correctly classified with 100% measurement consistency (1024/1024 shots each) |
| 04 | Grover's algorithm | Amplitude amplification | 2 | Measured: 100% (1024/1024 shots) vs theoretical 100% (exact resonance at k=1 iteration, N=4, M=1) |
| 05 | Grover's algorithm | Amplitude amplification, iteration-count scaling | 3 | Measured: 94.04% vs theoretical 94.5% |

## Background

Each notebook implements the algorithm from first principles in Qiskit and includes:
- the mathematical derivation of the circuit (state evolution in Dirac notation)
- an explanation of why the algorithm achieves its query/computational advantage
- construction and justification of the oracle, where applicable
- empirical measurement results compared against the closed-form theoretical prediction

The sequence is deliberate: Bell states establish entanglement and multi-qubit state
manipulation; Deutsch and Deutsch–Jozsa establish oracle-based query algorithms and the
classical/quantum separation; Grover (2- and 3-qubit) introduces amplitude amplification
and demonstrates how success probability scales with iteration count and qubit number.

## Repository structure

```
.
├── notebooks/
│   ├── 01_bell_state.ipynb
│   ├── 02_deutsch_algorithm.ipynb
│   ├── 03_deutsch_jozsa_nqubit.ipynb
│   ├── 04_grover_2qubit.ipynb
│   └── 05_grover_3qubit.ipynb
├── notes/
│   └── progress-log.md
├── papers/
├── assets/
├── requirements.txt
├── LICENSE
└── README.md
```

## Environment & reproducibility

- Python 3.13, Qiskit 2.4.1, Qiskit-Aer, Jupyter (see `requirements.txt` for pinned versions)
- **Known issue:** Qiskit-Aer has a reported import hang on Windows + Python 3.13 on
  first run; it resolves on its own. `StatevectorSampler` works as a fallback backend.

To reproduce:
```bash
python -m venv venv
source venv/bin/activate  # or venv\Scripts\activate on Windows
pip install -r requirements.txt
jupyter notebook notebooks/
```

## References

- Nielsen, M. & Chuang, I., *Quantum Computation and Quantum Information*, Ch. 1–4
- IBM Quantum Learning modules (Basics of Quantum Information, Quantum Algorithms)

## Roadmap

This repository is scoped to foundational, non-variational quantum algorithms. Follow-on
work extending these ideas to hybrid quantum-classical methods (Variational Quantum
Eigensolver for molecular systems) continues in a separate repository: [link once created].

## Development log

A week-by-week log of study and implementation notes is kept in
[`notes/progress-log.md`](notes/progress-log.md).

## License

MIT — see [LICENSE](LICENSE).
