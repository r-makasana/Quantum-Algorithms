# Quantum Teleportation

> Transfer a qubit's complete quantum state from one party to another using a shared entangled pair and two classical bits — without the qubit itself ever travelling.

## The problem (plain language)

Alice holds a qubit in some unknown state ψ. She wants Bob to end up with that exact state — amplitudes, phase, everything — but she can't send the qubit directly and she's not even allowed to look at it (measuring would destroy it). The question: is there a way to reconstruct ψ on Bob's side using only entanglement and ordinary classical communication?

Teleportation says yes: share one entangled pair in advance, let Alice perform two measurements on her side, send those two classical bits to Bob, and Bob applies at most two simple gates to recover ψ perfectly.

## The key idea

Three ingredients, in order:

1. **Shared entanglement** — Alice and Bob each hold one qubit of a Bell pair (|00⟩ + |11⟩)/√2, created before the protocol starts.
2. **Alice's move** — she entangles the message qubit with her half of the pair (CNOT), scrambles with a Hadamard, then measures both her qubits. This collapses everything, but the two classical bits she gets encode which of four possible "shifts" Bob's qubit has landed on.
3. **Bob's correction** — conditioned on Alice's two bits, Bob applies an X gate, a Z gate, both, or neither. After the correction, his qubit holds ψ exactly.

The critical point: Alice's two bits are uniformly random (~25% each of 00, 01, 10, 11) and carry zero information about ψ on their own. The state information is only recoverable when those bits are combined with Bob's entangled half. This is why teleportation doesn't transmit information faster than light — Bob's qubit is useless until the classical bits arrive.

## The circuit

![Teleportation circuit](teleportation_circuit.png)

Reading left to right:

| Stage | What happens |
|-------|-------------|
| **Initialize** | `qc.initialize(psi, 0)` loads a random input state onto q0. Uses `random_statevector(2)` so every run exercises a genuinely generic ψ. |
| **Bell pair** | H on q1 + CNOT(q1→q2) creates the shared entangled pair. q1 stays with Alice, q2 goes to Bob. |
| **Alice's gates** | CNOT(q0→q1) then H on q0 — entangles the message into the pair, then scrambles. |
| **Measure & send** | q0 → `crz`, q1 → `crx`. These are Alice's two classical bits. |
| **Bob's correction** | `if_test((crx, 1)): X(q2)` and `if_test((crz, 1)): Z(q2)` — Qiskit 2.x feed-forward, executed per-shot after Alice's measurement. |

## Run it

```bash
pip install -r ../../requirements.txt
jupyter notebook quantum_teleportation.ipynb
```

## What you should see

**Fidelity check:** `fidelity(Bob, psi) = 1.0` — computed by tracing out Alice's two qubits with `partial_trace` and comparing Bob's reduced state against the original ψ via `state_fidelity`. This holds for every random input state.

**Alice's bit histogram (8192 shots):**

| Outcome | Approximate % |
|---------|--------------|
| 0 0 | ~25% |
| 0 1 | ~25% |
| 1 0 | ~25% |
| 1 1 | ~25% |

The uniform distribution is the honesty check: Alice's bits are pure noise. They reveal nothing about ψ individually — the information only exists in the correlation between those bits and Bob's entangled qubit. This is why teleportation requires a classical channel and cannot violate relativity.

**Bloch sphere:** Bob's qubit arrow (q2) matches the arrow of the original ψ from Cell 2, visually confirming the state transfer.

## Does quantum actually help here?

Teleportation is a **protocol**, not a speedup algorithm. It doesn't do anything faster than classical communication — it does something classically *impossible*: faithfully transfer a continuous quantum state using only two discrete bits and pre-shared entanglement. No classical scheme can reconstruct an arbitrary qubit state from two bits alone.

That said, a classical copy of a known state is trivial. Teleportation's value is specifically for unknown states, and it's a foundational building block for quantum networking, error correction, and measurement-based computation — not a standalone performance claim.

## How correctness is verified

Two complementary checks, both run every time:

1. **Numerical fidelity** — `partial_trace` extracts Bob's qubit as a density matrix; `state_fidelity` compares it to the original ψ. A result of 1.0 means perfect transfer, and the check is phase-blind (handles global phase automatically). This runs across multiple random input states, not just one carefully chosen example.

2. **Alice-bit uniformity** — the histogram of Alice's two measurement outcomes over 8192 shots confirms ~25% per outcome. This isn't just a sanity check; it's the physical proof that Alice's bits alone carry no information about ψ, which is the core reason teleportation respects the no-communication theorem.

Both checks together confirm (a) the state arrived intact and (b) no information leaked through the classical channel — the two things teleportation promises.