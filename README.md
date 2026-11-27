# Superdense Coding

This project is a Qiskit simulation of superdense coding, a protocol that lets Alice send Bob two classical bits by transmitting only one qubit. It runs entirely on a simulator, so no quantum hardware is needed.

## The idea

A single qubit can normally carry only one bit of information, because measuring it gives a single 0 or 1. Superdense coding gets around this by using an entangled pair that Alice and Bob share in advance. Alice encodes her two-bit message by changing only her half of the pair and then sends that one qubit to Bob, who reads both bits by examining the two qubits together.

## How it works

Alice has four possible messages, and each one corresponds to a different operation on her qubit. For 00 she does nothing, for 01 she applies an X gate, for 10 she applies a Z gate, and for 11 she applies both. Each choice turns the shared pair into a different one of the four Bell states, which are distinct entangled states.

Once Bob receives Alice's qubit, he holds both halves of the pair. He applies a CNOT followed by an H gate, which turns each of the four Bell states into a plain two-bit result, and measuring the qubits then reveals Alice's message. The X gate shows up in the second bit and the Z gate shows up in the first.

## Why an eavesdropper learns nothing

The message is not stored in Alice's qubit on its own. It lives in the relationship between the two qubits, specifically in whether their values match and whether the state carries a plus or a minus sign. If Eve intercepts Alice's qubit and measures it, she gets 0 or 1 with equal probability no matter which message was sent, so she learns nothing. She can stop the message from arriving by keeping the qubit, but she cannot read it.

## Results

Each of the four messages is sent 1,000 times, and Bob decodes every one of them correctly. When Eve measures the intercepted qubit instead, her results are split roughly evenly between 0 and 1 for all four messages.

## Run it

```bash
pip install qiskit qiskit-aer matplotlib pylatexenc jupyter
jupyter notebook superdense_coding.ipynb
```

## Notes

Superdense coding is the mirror image of quantum teleportation. Teleportation uses an entangled pair and two classical bits to move the state of one qubit, while superdense coding uses an entangled pair and one qubit to send two classical bits. The entangled pair still has to be shared beforehand, so the total cost is two qubits for two bits, but one of those qubits can be delivered in advance, before the message is even decided.

Made with [Qiskit](https://www.ibm.com/quantum/qiskit).
