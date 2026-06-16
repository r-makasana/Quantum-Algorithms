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
| 3 | CHSH | *proving* the correlations aren't classical | Planned |
| 4 | Quantum Teleportation | moving a state via entanglement + classical bits | Planned |
| 5 | SuperDense Coding | two classical bits inside one qubit | Planned |
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
source .venv/bin/activate        # Windows: .venv\Scripts\activate

pip install -r requirements.txt
````

Python 3.10+ is recommended. Then open any folder's notebook:

````bash
jupyter notebook Tier-1-Entanglement-foundations/Bell-States/bell_states.ipynb
````

## Repo structure

````
quantum-algorithms/
├── README.md                         <- you are here
├── requirements.txt
├── Tier-1-Entanglement-foundations/
│   ├── Bell-States/
│   │   ├── README.md
│   │   ├── bell_states.ipynb
│   │   └── circuit.png
│   └── GHZ-States/
│       ├── README.md
│       ├── ghz_states.ipynb
│       └── ghz_circuit.png
├── Tier-2-Reversible-arithmetic/
├── Tier-3-Oracle-algorithms/
├── Tier-4-Fourier-and-walks/
└── Tier-5-Variational-and-QML/
````

## Built with

Qiskit · Qiskit Aer (simulation) · qiskit-ibm-runtime (real hardware) · the qiskit-algorithms / -optimization / -machine-learning ecosystem for the upper tiers.
````
````

A couple of choices worth flagging: I used plain "Done / Planned" text rather than status icons, and I kept the algorithm names matching your Tier folder structure. Update the two `Status` cells to "Done" as you finish each rung — that running progress bar is a nice signal to anyone browsing mid-build.

If you'd like, I can also generate the learning ladder as an actual image (SVG or PNG) you commit to the repo, so the landing page has a visual map instead of only the table. Otherwise, CHSH is the next rung whenever you're ready.