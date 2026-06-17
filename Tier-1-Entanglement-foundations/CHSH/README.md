# CHSH Inequality

> The experiment that turns "these qubits are entangled" into a measured number no classical universe can produce. It's the proof underneath Bell and GHZ.

## The problem (plain language)

Bell and GHZ states *look* entangled — but how do you rule out the boring explanation, that the two qubits secretly agreed on their answers in advance? That "pre-arranged answers" idea is a local hidden-variable model: the quantum version of two coins glued to always match.

CHSH (Clauser–Horne–Shimony–Holt) settles it with a score. Alice and Bob each hold one qubit of an entangled pair, in separate rooms. Each independently picks one of two measurements and records +1 or −1. From how their results correlate across the four measurement combinations, you compute a single number, **S**.

## The key idea

- If the qubits carried pre-set answers — any classical, local model — then **|S| ≤ 2**. No exceptions.
- Quantum mechanics, with the right measurement angles on an entangled pair, reaches **|S| ≤ 2√2 ≈ 2.828** (Tsirelson's bound).

Measuring S > 2 rules out *every* local hidden-variable explanation at once. That is the result.

The four correlations combine as:

````
S = E(A0,B0) − E(A0,B1) + E(A1,B0) + E(A1,B1)
````

where each `E` is `[N(00) + N(11) − N(01) − N(10)] / shots` for one pair of settings. A "measurement at angle θ" is an `Ry(θ)` rotation on the qubit before a normal Z-basis measurement. The angles that reach the maximum:

- Alice: `0` and `π/2`
- Bob: `π/4` and `3π/4`

## Run it

````bash
pip install -r ../../requirements.txt
jupyter notebook chsh.ipynb
````

## What you should see

Each of the four setting-circuits runs at 8192 shots. The four correlations land near ±0.707 and combine to:

````
S ≈ 2.82
````

— comfortably past the classical ceiling of 2 and within shot noise of Tsirelson's 2.828. Don't expect exactly 2.828; the small gap is statistical.

## Does quantum actually help here?

No algorithm, no speedup — but this is the most important honesty entry in Tier 1. CHSH doesn't *use* entanglement to compute something faster; it *proves* the entanglement is real and non-classical. Every speedup later in this repo ultimately rests on the kind of correlation CHSH verifies here.

## How correctness is verified

Two states, one protocol:

1. **Entangled pair → violation.** S climbs to ~2.82, breaking the classical bound of 2.
2. **Separable control → no violation.** The identical protocol on a non-entangled product state (`|00⟩`, entangler removed) collapses S to ~1.4, safely under 2. This control is the proof: the violation comes from entanglement and nothing else.