# BB84 QKD Simulation (Qiskit)

Simulation of the BB84 quantum key distribution protocol using Qiskit and Qiskit Aer. Implemented in June 2026 as a follow-up to my Grover's algorithm notebook.

## What this does

BB84 (Bennett and Brassard, 1984) lets Alice and Bob agree on a shared secret key by sending qubits, such that an eavesdropper can be detected. I wanted to see the no-cloning theorem actually show up in code instead of just reading about it, so I simulated the whole protocol:

- Alice picks random bits and random bases (rectilinear or diagonal) and encodes the qubits
- Bob measures in his own random bases
- They keep only the positions where the bases matched (sifting)
- They compare a sample of the key to estimate the error rate
- Case 1: no eavesdropper. Case 2: Eve intercepts and resends

## Result

<!-- fill with YOUR numbers from the notebook -->
Without Eve, the error rate in the sifted key was 0.00%. With Eve intercepting every qubit, it was 50.00% (theory says around 25% for intercept-resend). This is what lets Alice and Bob detect her.

## What I took from it

- BB84 only detects eavesdropping, it does not prevent it. Eve still gets to try.
- Eve doesn't even need the key. If she just keeps intercepting, the error rate stays high and Alice and Bob can never build a key. So the protocol *protects confidentiality but not availability* (a denial of service).
- Even if key cannot be made, the high error rate still tells them the channel is being watched. It works like a fuse.

## Files

- `BB84.ipynb`: the simulation with code, test runs and my notes
- `bases.png`: diagram of the two bases, rectilinear (|0>, |1>) and diagonal (|+>, |->)
- `requirements.txt`: qiskit, qiskit-aer, numpy

## Running it

pip install -r requirements.txt, then open the notebook in Jupyter.

## Limitations

This is a simulator with ideal qubits, no channel noise, and only intercept-resend attacks. It is a learning project, not a usable QKD library.
