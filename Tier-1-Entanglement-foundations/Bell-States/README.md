# Bell States
> This circuit demonstrates the creation of all four Bell states using a single shared entangler.

## The Problem (Plain Language)
How can we link two independent qubits so that they share a single quantum state, and how do we create the four distinct versions (Bell states) of this entanglement?

## The Key Idea
[cite_start]Instead of building four separate circuits, we use one "entangling primitive" (a Hadamard gate followed by a CNOT gate)[cite: 93, 128]. [cite_start]By applying different bit-flip (X) gates to the inputs *before* they enter the entangler, we can produce any of the four Bell states ($\Phi^+, \Phi^-, \Psi^+, \Psi^-$)[cite: 90, 151].

## The Circuit
![circuit](circuit.png)
[cite_start]The circuit applies an initial preparation step (if needed) followed by the shared H + CNOT entangler[cite: 93].

# Open the bell_states.ipynb notebook to see the verification results.