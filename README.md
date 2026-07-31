![Python](https://img.shields.io/badge/Python-3.13-blue)
![License](https://img.shields.io/badge/License-MIT-green)
![Qiskit](https://img.shields.io/badge/Qiskit-2.4.1-purple)

# Quantum Algorithms: Foundations

This repository implements and validates several of the foundational algorithms of quantum computation using Qiskit.
Rather than simply reproducing textbook circuits, each notebook develops the mathematical framework behind the algorithm, constructs the quantum circuit from first principles, and compares simulation results with theoretical predictions.
This repository was developed independently alongside my undergraduate Physics studies as part of a broader interest in computational physics and quantum computing.

## Overview
| # | Algorithm | Concept demonstrated | Qubits | Validation Results |
|---|-----------|----------------------|--------|------------|
| 01 | Bell state | Entanglement, superposition | 2 | 50.6% \|00⟩ / 49.4% \|11⟩, 0% leakage into \|01⟩/\|10⟩ (1000 shots) — consistent with ideal Bell state within statistical noise |
| 02 | Deutsch's algorithm | Query complexity separation, oracle design | 1 | All 4 oracle cases verified against expected output |
| 03 | Deutsch–Jozsa (n-qubit) | Generalised oracle, exponential classical/quantum query gap | n = 2, 3, 4 | Constant (f=0, f=1) and balanced oracles correctly classified with 100% measurement consistency at every tested n (1024/1024 shots each) |
| 04 | Grover's algorithm | Amplitude amplification | 2 | Measured: 100% (1024/1024 shots) vs theoretical 100% (exact resonance at k=1 iteration, N=4, M=1) |
| 05 | Grover's algorithm | Amplitude amplification, iteration-count scaling | 3 | Measured: 94.04% vs theoretical 94.5% |

## Objectives

Each notebook aims to:
- derive the mathematical foundations of the algorithm
- construct the corresponding quantum circuit from first principles
- validate simulation results against theoretical predictions
- explain the source of the algorithm's quantum advantage

## Learning progression

| Stage         | Concept                        |
| ------------- | ------------------------------ |
| Bell states   | Superposition and entanglement |
| Deutsch       | Oracle-based computation       |
| Deutsch–Jozsa | Quantum query complexity       |
| Grover        | Amplitude amplification        |


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

Tested using:
- Python 3.13
- Qiskit 2.4.1
- Qiskit Aer

**Known issue:** Qiskit-Aer has a reported import hang on Windows + Python 3.13 on
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
- Grover, L. K. (1996). A fast quantum mechanical algorithm for database search.

## Future Work

Potential extensions include:
- Quantum Fourier Transform
- Quantum Phase Estimation
- Variational Quantum Eigensolver
- Quantum Approximate Optimization Algorithm (QAOA)

## Development log

A week-by-week log of study and implementation notes is kept in
[`notes/progress-log.md`](notes/progress-log.md).

## License

MIT — see [LICENSE](LICENSE).
