# 7. Implications, P vs NP, and Coping Strategies

## 7.1 The P vs NP Question

> **The question:** Is P = NP?
>
> Equivalently: can every problem whose solution can be *verified* in polynomial time also be *solved* in polynomial time?

### What we know

| Fact | Status |
|------|--------|
| P ⊆ NP | Proved (trivially) |
| P ⊊ EXP | Proved (time hierarchy theorem) |
| P = NP or P ≠ NP | **Open** — one of the seven Millennium Prize Problems ($1M prize) |

### Expert consensus

Most complexity theorists believe P ≠ NP. An informal poll at a 2019 conference found roughly 80% believe P ≠ NP, with most expecting no proof in their lifetimes.

### Consequences if P = NP

- Every NP-complete problem would be solvable in polynomial time.
- Cryptography based on computational hardness (RSA, Diffie-Hellman, etc.) would collapse.
- Optimisation, scheduling, logistics — all become efficiently solvable.
- Mathematical proofs could be found as easily as verified (since proof verification is in P, proof finding would be too).

### Consequences if P ≠ NP (the expected case)

- NP-complete problems have no polynomial-time algorithms.
- Computational hardness is a genuine phenomenon, not just a reflection of our ignorance.
- Cryptographic security has a firm theoretical foundation.

---

## 7.2 Barriers to Proving P ≠ NP

Several meta-theorems show that certain proof techniques cannot resolve P vs NP:

| Barrier | Year | Rules out |
|---------|------|-----------|
| Relativisation (Baker-Gill-Solovay) | 1975 | Proofs that work relative to all oracles |
| Natural proofs (Razborov-Rudich) | 1997 | A broad class of combinatorial arguments (assuming one-way functions exist) |
| Algebrisation (Aaronson-Wigderson) | 2009 | Proofs that "algebrise" — extend to algebraic oracles |

Any proof of P ≠ NP must use fundamentally new techniques that bypass all three barriers.

---

## 7.3 Coping with NP-Hardness

When you encounter an NP-hard problem in practice, you have several options:

### Strategy 1: Exact algorithms for small inputs

Brute-force or clever exponential algorithms may be fast enough when n is small.

| Algorithm | Time | Problem |
|-----------|------|---------|
| Brute-force SAT | O(2ⁿ) | SAT |
| Dynamic programming | O(n² 2ⁿ) | TSP |
| Branch and bound | Varies | Many combinatorial problems |

### Strategy 2: Approximation algorithms

Accept a solution that is provably close to optimal.

| Problem | Approximation ratio | Algorithm |
|---------|-------------------|-----------|
| Vertex Cover | 2 | Take both endpoints of a maximal matching |
| Metric TSP | 3/2 | Christofides' algorithm |
| Set Cover | O(log n) | Greedy |
| MAX-3-SAT | 7/8 | Random assignment |

**Caveat:** Some problems are NP-hard to approximate beyond a certain ratio (e.g., Clique cannot be approximated within n^{1-ε} unless P = NP).

### Strategy 3: Parameterised complexity (FPT)

If some parameter k of the instance is small, there may be an algorithm running in O(f(k) · n^c) time — exponential in k but polynomial in n.

| Problem | Parameter k | FPT algorithm |
|---------|-------------|---------------|
| Vertex Cover | Cover size | O(2^k · n) |
| k-Clique | Clique size | O(n^k) — not FPT; but colour-coding gives randomised FPT |
| SAT | Treewidth of clause–variable graph | O(2^{tw} · n) |

### Strategy 4: Heuristics and metaheuristics

No worst-case guarantees, but often work well in practice:
- SAT solvers (DPLL, CDCL) — solve industrial instances with millions of variables
- Local search (simulated annealing, tabu search)
- Evolutionary algorithms / genetic algorithms
- Integer linear programming (ILP) solvers (branch-and-cut)

### Strategy 5: Special cases

Many NP-complete problems become polynomial on restricted inputs:
- SAT → 2-SAT is in P (linear time)
- Colouring → 2-colouring is in P (bipartiteness check)
- Hamiltonian Cycle → on tournament graphs, always exists
- TSP → Euclidean TSP has a PTAS
- Independent Set → on trees, bipartite, or interval graphs → polynomial

### Strategy 6: Average-case vs worst-case

NP-hardness is a worst-case statement. Many NP-complete problems are easy on "typical" random instances. Phase transitions in random SAT, random graphs, etc., give structure that algorithms can exploit.

---

## 7.4 Beyond NP: The Polynomial Hierarchy

NP is just the first level of a richer structure:

```
        Σ₃ᵖ ∪ Π₃ᵖ
       ╱          ╲
     Σ₃ᵖ          Π₃ᵖ         Level 3: ∃∀∃ / ∀∃∀
       ╲          ╱
        Σ₂ᵖ ∪ Π₂ᵖ
       ╱          ╲
     Σ₂ᵖ          Π₂ᵖ         Level 2: ∃∀ / ∀∃
       ╲          ╱
        NP ∪ coNP
       ╱          ╲
     NP            coNP        Level 1: ∃ / ∀
       ╲          ╱
           P                   Level 0
```

- Σ₁ᵖ = NP, Π₁ᵖ = coNP
- PH = ⋃ᵢ Σᵢᵖ (the polynomial hierarchy)
- If any level of PH collapses (Σᵢᵖ = Πᵢᵖ), then PH collapses to that level
- If P = NP, the entire PH collapses to P

---

## 7.5 Key Takeaways

1. **NP-completeness is a classification tool.** When you prove your problem NP-complete, you know to stop looking for an efficient exact algorithm and start looking for approximations, heuristics, or special cases.

2. **Reductions are the glue.** The entire theory rests on polynomial-time reductions connecting thousands of problems into one equivalence class.

3. **The Cook-Levin theorem is the foundation.** It provides the first NP-complete problem (SAT) from which all others are derived.

4. **P vs NP is still open.** But the practical implications of NP-hardness are clear: use approximation, parameterisation, heuristics, or exploit structure.

5. **NP-hardness is worst-case.** Many hard problems are easy in practice for structured inputs. Modern SAT solvers, ILP solvers, and constraint solvers routinely handle enormous instances.

---

## 7.6 Further Reading

- Sipser, *Introduction to the Theory of Computation* — accessible textbook
- Arora & Barak, *Computational Complexity: A Modern Approach* — comprehensive graduate text
- Garey & Johnson, *Computers and Intractability* — the classic reference for NP-completeness
- Karp (1972), "Reducibility among Combinatorial Problems" — the original 21 NP-complete problems
- Cook (1971), "The Complexity of Theorem-Proving Procedures" — the original proof that SAT is NP-complete
