# 🔱 Cryzene Protocol

> _Post-Quantum Byzantine Agreement via Autovectorized, Privacy-Preserving Cryptographic Computation._

**Cryzene** is a research-grade, fully software-implemented cryptographic framework that establishes **Byzantine fault-tolerant consensus** over encrypted data in **partially synchronous networks**, even under quantum adversaries. The protocol fuses recent advances in **post-quantum cryptography**, **homomorphic encryption**, **tensorized computation**, **compiler-driven autovectorization**, and **doubly-efficient Private Information Retrieval (PIR)** to provide a secure, portable, and efficient software stack for consensus in hostile or low-trust environments.

Cryzene emphasizes _software-only_ performance: all cryptographic operations are accelerated via finite-field SIMD-like arithmetic and autovectorized tensor transformations—no hardware acceleration or trusted setup is required.

---

## 🧬 Architecture Overview

Cryzene simulates a secure distributed system composed of:

- **Clients / Nodes**:
  - Establish quantum-secure communication using **Kyber** (Module-LWE).
  - Sign consensus messages using **SQIsign** (isogeny-based signatures).
  - Query remote databases privately via **LWE-based PIR**.
  - Perform homomorphic computations on encrypted tensors.
  - Reach Byzantine Agreement using an **O(f)-round, O(f²)-message BA protocol**.

- **Server**:
  - Stores PIR-queryable encrypted data.
  - Executes **homomorphic computations** over tensor-structured ciphertexts.
  - Optimizes HE transformations using a **custom compiler for autovectorized tensor ops**.

- **Network**:
  - Simulated partial synchrony with minimal timing guarantees.
  - All communication is encrypted (Kyber) and authenticated (SQIsign).

---

## 📦 Core Components & Jargon Stack

| Module | Description |
|--------|-------------|
| `cryzene-arith` | Fast modular arithmetic engine using pseudo-Mersenne primes and pipeline-aware register scheduling. |
| `cryzene-tensor` | Tensor-based abstraction over cryptographic data (Kyber polynomials, HE ciphertexts), aligned for vectorization. |
| `cryzene-he` | Lightweight homomorphic encryption layer (BFV/CKKS-style), operating over tensor layouts. |
| `cryzene-compiler` | Static optimization layer transforming encrypted tensor programs using **ApplyRoll-style layout transformations** and **loop-level autovectorization** (inspired by Rotom). |
| `cryzene-pir` | LWE-based **doubly-efficient** PIR engine using matrix-vector multiplication with precomputed query compression (SODA’07 inspired). |
| `cryzene-ba` | Byzantine Agreement protocol with minimal synchrony assumptions, cryptographically hardened using Kyber + SQIsign. |
| `cryzene-core` | Simulation environment with async clients, message queues, and performance instrumentation. |

---

## 🔬 Key Concepts

- **Autovectorization**: Cryzene uses a compiler pass to restructure encrypted tensor operations into vectorized loops, minimizing rotations and memory shuffles across ciphertext slots.
  
- **Tensorized Cryptography**: Cryptographic primitives (e.g., NTT in Kyber, plaintext packing in HE) are executed using multi-dimensional tensor structures aligned to cache lines and SIMD register widths.

- **Post-Quantum Security**: All encryption and signature primitives are resistant to known quantum algorithms, using hybrid cryptography (Kyber + SQIsign).

- **Byzantine Agreement**: Consensus under partial synchrony is achieved with theoretical bounds of O(f) rounds, O(f²) communication, and resilience to Byzantine adversaries.

- **Private Information Retrieval (PIR)**: Clients query a remote encrypted dataset without revealing their access pattern, using LWE-encrypted queries and vectorized response generation.

---

## 🛠️ Example Use Case

> _“Privacy-preserving consensus on encrypted sensor data in a quantum-vulnerable, adversarial network”_

1. Nodes securely retrieve encrypted analytics via PIR.
2. HE engine performs summation and statistical aggregation.
3. Autovectorized compiler minimizes ciphertext-level computation overhead.
4. Results are verified and agreed upon using the Byzantine Agreement layer.

---

## 📁 Project Layout (Workspace Overview)

```bash
cryzene/
├── cryzene-arith/       # Modular reduction, finite field ops (Rust + SIMD)
├── cryzene-tensor/      # Tensor abstraction layer
├── cryzene-he/          # Homomorphic encryption engine
├── cryzene-compiler/    # HE tensor compiler (ApplyRoll & vectorization)
├── cryzene-pir/         # Doubly-efficient PIR engine
├── cryzene-ba/          # Byzantine Agreement over secure channels
├── cryzene-core/        # Integration testbed and network simulator
├── examples/            # Mini-protocol demos and benchmarks
└── README.md

