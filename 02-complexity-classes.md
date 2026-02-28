# 2. Complexity Classes

We now use the Turing machine framework to define the central complexity classes.

---

## 2.1 DTIME and the Class P

> **Definition.** For a function t: ℕ → ℕ,
>
> **DTIME(t(n))** = { L : there exists a DTM that decides L in O(t(n)) steps }

> **Definition.** **P** (polynomial time) is the class
>
> P = ⋃_{k ≥ 0} DTIME(n^k)
>
> i.e., all languages decidable by a DTM in time polynomial in the input size.

### Why P matters

P is the formal analogue of "efficiently solvable." A problem in P has an algorithm whose running time is bounded by some polynomial n^k. While n^{100} is technically polynomial, in practice P problems tend to have low-degree polynomial algorithms.

### Examples of problems in P

| Problem | Best known bound |
|---------|-----------------|
| Sorting | O(n log n) |
| Shortest path (Dijkstra) | O(n² ) or O(m + n log n) |
| 2-SAT | O(n + m) |
| Linear programming | Polynomial (ellipsoid/interior point) |
| Primality testing (AKS) | O(n^6) where n = number of digits |
| Maximum matching | O(n^{1/2} m) |

---

## 2.2 NTIME and the Class NP

> **Definition.**
>
> **NTIME(t(n))** = { L : there exists an NTM that decides L in O(t(n)) steps }

> **Definition.** **NP** (non-deterministic polynomial time) is
>
> NP = ⋃_{k ≥ 0} NTIME(n^k)

### Equivalent "verifier" definition

This is the definition most people encounter first and is equivalent to the NTM definition:

> **Definition (Verifier).** A language L is in **NP** if and only if there exists a polynomial-time DTM V (the *verifier*) and a polynomial p such that:
>
> L = { w : ∃ certificate c with |c| ≤ p(|w|) such that V(w, c) accepts }
>
> - **Completeness:** If w ∈ L, there exists a certificate c that makes V accept.
> - **Soundness:** If w ∉ L, no certificate makes V accept.

### Why the two definitions are equivalent

- **NTM → Verifier:** If an NTM accepts w in polynomial time, the sequence of non-deterministic choices is a polynomial-length certificate. A DTM verifier can replay the NTM computation along that specific path.
- **Verifier → NTM:** An NTM can non-deterministically guess the certificate c, then run the deterministic verifier V(w, c).

### Intuition

NP = the class of problems where **solutions can be verified quickly** (in polynomial time), even if finding a solution might be hard.

### Examples of problems in NP

| Problem | Certificate |
|---------|-------------|
| SAT | A satisfying assignment |
| Hamiltonian Cycle | The cycle itself (a permutation of vertices) |
| Graph Colouring (k colours) | The colouring |
| Subset Sum | The subset |
| Clique | The clique vertices |
| Travelling Salesman (decision) | The tour |

---

## 2.3 The Relationship P ⊆ NP

> **Theorem.** P ⊆ NP.

*Proof.* If L ∈ P, there is a poly-time DTM M deciding L. Construct a verifier V that ignores the certificate and just runs M on w. Then V runs in polynomial time, so L ∈ NP. ∎

The **P vs NP question** asks whether P = NP or P ⊊ NP. This is the most important open problem in theoretical computer science (and one of the Millennium Prize Problems).

---

## 2.4 coNP

> **Definition.** **coNP** = { L : L̄ ∈ NP }
>
> where L̄ = Σ* \ L is the complement of L.

A problem is in coNP if **no-instances** have short, efficiently verifiable proofs.

**Example:** TAUTOLOGY (is a Boolean formula true under every assignment?) is in coNP. A falsifying assignment is a short certificate for the complement (SAT).

**Known relationships:**
- P ⊆ NP ∩ coNP
- If NP ≠ coNP, then P ≠ NP (contrapositive: P = NP ⟹ NP = coNP)

---

## 2.5 EXP

> **Definition.** **EXP** (exponential time) is
>
> EXP = ⋃_{k ≥ 0} DTIME(2^{n^k})

**Known:** P ⊆ NP ⊆ EXP, and P ⊊ EXP (by the time hierarchy theorem).

---

## 2.6 The Landscape

```
┌─────────────────────────────────────────────────┐
│                      EXP                        │
│  ┌───────────────────────────────────────────┐  │
│  │                   NP                      │  │
│  │  ┌─────────────────────────────────────┐  │  │
│  │  │               P                     │  │  │
│  │  │                                     │  │  │
│  │  │   Sorting, Shortest Path, 2-SAT,   │  │  │
│  │  │   Matching, Primality, LP           │  │  │
│  │  │                                     │  │  │
│  │  └─────────────────────────────────────┘  │  │
│  │                                           │  │
│  │   SAT, Clique, Ham. Cycle, TSP,          │  │
│  │   3-Colouring, Subset Sum                │  │
│  │   (NP-complete — if P ≠ NP these are     │  │
│  │    outside P)                             │  │
│  └───────────────────────────────────────────┘  │
│                                                 │
│   Problems known to be outside NP (assuming     │
│   standard conjectures), e.g., some games       │
└─────────────────────────────────────────────────┘
```

---

## 2.7 Summary

| Class | Defined by | Intuition |
|-------|-----------|-----------|
| P | Poly-time DTM | Efficiently solvable |
| NP | Poly-time NTM (or verifier + certificate) | Efficiently verifiable |
| coNP | Complement of NP | "No" answers efficiently verifiable |
| EXP | Exponential-time DTM | Solvable with brute force |

**Next:** [Chapter 3 — Reductions](03-reductions.md)
