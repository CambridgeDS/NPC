# 3. Polynomial-Time Reductions

Reductions are the central tool for comparing the difficulty of problems. If problem A reduces to problem B, then B is "at least as hard" as A.

---

## 3.1 Many-One (Karp) Reductions

> **Definition.** Language A is *polynomial-time many-one reducible* to language B, written
>
> A ≤_p B
>
> if there exists a polynomial-time computable function f: Σ* → Σ* such that for every w:
>
> w ∈ A ⟺ f(w) ∈ B

### Properties

| Property | Statement |
|----------|-----------|
| Reflexive | A ≤_p A (use f = identity) |
| Transitive | If A ≤_p B and B ≤_p C, then A ≤_p C (compose the two functions) |
| NOT symmetric | A ≤_p B does NOT imply B ≤_p A |

### The key consequence

> **Theorem.** If A ≤_p B and B ∈ P, then A ∈ P.

*Proof.* Given input w for A:
1. Compute f(w) in polynomial time.
2. Run the polynomial-time algorithm for B on f(w).
3. Accept iff the B-algorithm accepts.

Total time: poly(|w|) + poly(|f(w)|) = poly(|w|) (since |f(w)| ≤ poly(|w|)). ∎

**Contrapositive:** If A ≤_p B and A ∉ P, then B ∉ P. This is how we prove problems are hard.

---

## 3.2 Turing (Cook) Reductions

> **Definition.** A is *polynomial-time Turing reducible* to B, written A ≤_T B, if there exists a polynomial-time algorithm for A that can make calls to an **oracle** for B.

- More powerful than Karp reductions (can make multiple oracle calls, can negate the answer).
- A ≤_p B implies A ≤_T B, but not vice versa.
- Karp reductions are preferred for NP-completeness proofs because they preserve membership in NP.

---

## 3.3 How to Construct a Reduction

When proving A ≤_p B, you must:

1. **Design** the function f that maps instances of A to instances of B.
2. **Prove correctness:**
   - (⟹) If w ∈ A, then f(w) ∈ B.
   - (⟸) If f(w) ∈ B, then w ∈ A.
3. **Prove efficiency:** f is computable in polynomial time.

### Example: INDEPENDENT-SET ≤_p CLIQUE

- **INDEPENDENT-SET:** Given graph G = (V, E) and integer k, does G have an independent set of size ≥ k?
- **CLIQUE:** Given graph G = (V, E) and integer k, does G have a clique of size ≥ k?

**Reduction f:** Given (G, k), output (Ḡ, k) where Ḡ is the complement graph (same vertices, edge ↔ non-edge).

**Correctness:** S is an independent set in G ⟺ S is a clique in Ḡ.

**Efficiency:** Computing Ḡ takes O(|V|²) time. ✓

---

## 3.4 The Reduction Diagram

A typical chain of reductions used to prove NP-completeness looks like:

```
SAT
 │
 ▼
3-SAT
 │
 ├──────────────┐
 ▼              ▼
CLIQUE    INDEPENDENT SET
 │
 ▼
VERTEX COVER
 │
 ▼
SET COVER
```

Each arrow A → B means A ≤_p B. If SAT is NP-complete, then every problem reachable by a chain of reductions from SAT is also NP-hard.

---

## 3.5 Common Pitfalls

**Direction matters.** To show B is hard, you reduce a known hard problem A **to** B:

```
Known hard problem A  ≤_p  Target problem B
```

NOT the other way around. Reducing B to A would show B is *easier* than A.

**The reduction itself must be efficient.** The function f must run in polynomial time. You cannot use an exponential-time reduction — that would prove nothing.

**Correctness is bidirectional.** You must show both directions of the if-and-only-if. A common mistake is only showing one direction.

---

## 3.6 Summary

| Concept | Notation | Meaning |
|---------|----------|---------|
| Karp reduction | A ≤_p B | Poly-time computable f: w ∈ A ⟺ f(w) ∈ B |
| Cook reduction | A ≤_T B | Poly-time algorithm for A with oracle for B |
| Direction | A ≤_p B | "B is at least as hard as A" |
| Key theorem | If A ≤_p B and B ∈ P, then A ∈ P | Hardness transfers upward through reductions |

**Next:** [Chapter 4 — NP-Hardness and NP-Completeness](04-np-hardness.md)
