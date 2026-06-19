# Quantum Algorithms

> A hands-on tour of quantum computing in Qiskit, built one algorithm at a time. Every folder is self-contained — a plain-language explanation, a working circuit, and an honest take on whether quantum actually helps.

## What this is

A learning ladder, not a grab-bag. The algorithms are ordered so each one only needs concepts from the ones before it: start with two entangled qubits, end with hybrid quantum machine learning. Each folder is written so someone with no quantum background can understand the idea in about two minutes, and every folder ends with the same blunt question — *does quantum actually help here?* — answered honestly, including the cases where the answer is "not yet."

Two threads run through the whole repo:

- **Honesty over hype.** Foundations are labelled as primitives, not speedups. Where a classical method does the same job, it's named.
- **Verification as the default.** Every circuit is checked, not just run — measured distributions against expectations, plus statevector/Q-sphere inspection for the phase information that measurement hides.

## The learning ladder

| # | Algorithm | What it teaches | Status |
|---|-----------|-----------------|--------|
| **Tier 1 — Entanglement foundations** | | | |
| 1 | Bell States | superposition, entanglement, correlated measurement | Done |
| 2 | GHZ States | entanglement across three or more qubits | Done |
| 3 | CHSH | *proving* the correlations aren't classical | Done |
| 4 | Quantum Teleportation | moving a state via entanglement + classical bits | Done |
| 5 | SuperDense Coding | two classical bits inside one qubit | Done |
| **Tier 2 — Reversible arithmetic** | | | |
| 6 | Increment Circuit | controlled gates as reversible arithmetic | Planned |
| 7 | Decrement Circuit | reversible subtraction | Planned |
| **Tier 3 — Oracle algorithms** | | | |
| 8 | Deutsch–Josza | first clear quantum advantage; oracles + phase kickback | Planned |
| 9 | Bernstein–Vazirani | recovering a hidden bit-string in one query | Planned |
| 10 | Grover's Search | amplitude amplification; quadratic speedup | Planned |
| **Tier 4 — Fourier & walks** | | | |
| 11 | Quantum Fourier Transform | the subroutine the advanced algorithms are built on | Planned |
| 12 | Quantum Random Walks | quantum vs. classical diffusion | Planned |
| **Tier 5 — Variational & quantum ML** | | | |
| 13 | QAOA | hybrid quantum-classical optimization | Planned |
| 14 | QSVM | quantum kernels for classification | Planned |
| 15 | QGANs | quantum generative models | Planned |

## How each folder is organized

Every algorithm folder follows the same structure, so once you've read one you know where to look in all of them:

- **The problem** — what question we're answering, in plain language
- **The key idea** — the one trick that makes it work
- **The circuit** — a diagram, with a line on what each part does
- **Run it** — how to reproduce the result
- **What you should see** — the expected output and why it looks that way
- **Does quantum actually help?** — the honest comparison to the classical approach
- **How correctness is verified** — the checks that back up the claim

## Getting started

````bash
git clone https://github.com/r-makasana/quantum-algorithms.git
cd quantum-algorithms

python -m venv .venv
source .venv/bin/activate        # Windows: source .venv/Scripts/activate

pip install -r requirements.txt
````

Python 3.10+ is recommended. Then open any folder's notebook:

````bash
jupyter notebook Tier-1-Entanglement-foundations/Bell-States/bell_states.ipynb
````

## Repo structure

````
quantum-algorithms/
├── README.md                        
├── requirements.txt
├── Tier-1-Entanglement-foundations/
│   ├── Bell-States/
│   │   ├── README.md
│   │   ├── bell_states.ipynb
│   │   └── circuit.png
│   ├── GHZ-States/
│   │   ├── README.md
│   │   ├── ghz_states.ipynb
│   │   └── ghz_circuit.png
│   |── CHSH/
│   |   ├── README.md
│   |   ├── chsh.ipynb
│   |   └── chsh_circuit.png
|   |── Quantum-Teleportation/
│   |   ├── README.md
│   |   ├── quantum_teleportation.ipynb
│   |   └── teleportation_circuit.png
|   |── Superdense-Coding/
│   |   ├── README.md
│   |   ├── superdense_coding.ipynb
│   |   ├── superdense_coding_circuit.png
│   |   ├── superdense_coding_results_simulator.png
│   |   └── superdense_coding_results_realhardware.png
├── Tier-2-Reversible-arithmetic/
├── Tier-3-Oracle-algorithms/
├── Tier-4-Fourier-and-walks/
└── Tier-5-Variational-and-QML/
````

