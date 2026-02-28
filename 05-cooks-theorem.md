# 5. The Cook-Levin Theorem

The Cook-Levin theorem (Cook, 1971; Levin, 1973, independently) establishes the first NP-complete problem and bootstraps the entire theory.

---

## 5.1 The SAT Problem

> **Definition (SAT).** Given a Boolean formula φ in conjunctive normal form (CNF), is there an assignment to the variables that makes φ true?

A CNF formula is a conjunction (AND) of clauses, where each clause is a disjunction (OR) of literals:

```
φ = (x₁ ∨ ¬x₂ ∨ x₃) ∧ (¬x₁ ∨ x₄) ∧ (x₂ ∨ ¬x₃ ∨ ¬x₄ ∨ x₅)
```

---

## 5.2 Statement

> **Theorem (Cook-Levin).** SAT is NP-complete.

This requires two parts:
1. SAT ∈ NP.
2. For every L ∈ NP, L ≤_p SAT.

---

## 5.3 SAT ∈ NP

- **Certificate:** An assignment α: {x₁, ..., x_n} → {0, 1}.
- **Verification:** Evaluate φ under α. Check each clause has at least one true literal.
- **Time:** O(|φ|) — linear in the formula size. ✓

---

## 5.4 Every NP Problem Reduces to SAT (Proof Sketch)

This is the deep part. The idea: **encode the entire computation of an NTM as a Boolean formula**.

Let L ∈ NP. Then there exists an NTM M that decides L in time p(n) for some polynomial p.

Given input w of length n, we construct a formula φ_w that is satisfiable if and only if M accepts w. The construction uses the following variables:

### Variables

| Variable | Meaning |
|----------|---------|
| cell_{i,j,s} | At time step i, tape cell j contains symbol s |
| head_{i,j} | At time step i, the head is at position j |
| state_{i,q} | At time step i, the machine is in state q |

Here i ranges from 0 to T = p(n), j ranges from -T to T, s ranges over Γ, and q ranges over Q. Total number of variables: O(T² · (|Γ| + |Q|)) = polynomial in n.

### Clauses

The formula φ_w is the conjunction of clauses encoding:

1. **Initial configuration:** At time 0, the tape contains w, the head is at position 0, and the state is q₀.

2. **At most / exactly one:** At each time step, the machine is in exactly one state, the head is at exactly one position, and each cell contains exactly one symbol.

3. **Transition relation:** For each time step i, the next state, head position, and symbol written are consistent with δ. This is where non-determinism is handled — for an NTM, the formula allows any one of the valid transitions.

4. **Acceptance:** At some time step i ≤ T, the machine is in state q_accept.

5. **Inertia:** Tape cells not under the head do not change between consecutive steps.

### Correctness

- **(⟹)** If M accepts w, there is an accepting computation path. The configuration at each step gives a satisfying assignment to the variables.
- **(⟸)** If φ_w is satisfiable, the assignment describes a valid accepting computation of M on w, so w ∈ L.

### Efficiency

- The number of variables is O(T²) = O(p(n)²) — polynomial.
- The number of clauses is O(T²) — polynomial.
- The construction is computable in polynomial time. ✓

---

## 5.5 3-SAT is NP-Complete

> **Definition (3-SAT).** SAT restricted to formulas where every clause has exactly 3 literals.

> **Theorem.** 3-SAT is NP-complete.

*Proof sketch of SAT ≤_p 3-SAT.* Any clause with k > 3 literals can be broken into equivalent 3-literal clauses by introducing O(k) fresh variables:

```
(ℓ₁ ∨ ℓ₂ ∨ ℓ₃ ∨ ℓ₄ ∨ ℓ₅)
```
becomes:
```
(ℓ₁ ∨ ℓ₂ ∨ y₁) ∧ (¬y₁ ∨ ℓ₃ ∨ y₂) ∧ (¬y₂ ∨ ℓ₄ ∨ ℓ₅)
```

Clauses with 1 or 2 literals are padded with dummy variables. The resulting formula has O(|φ|) clauses, each with exactly 3 literals, and is satisfiable iff the original is. ∎

**Note:** 2-SAT is in P (solvable in linear time). So the jump from 2 to 3 literals crosses the P/NP-complete boundary (assuming P ≠ NP).

---

## 5.6 Why Cook-Levin Matters

1. **It provides the seed.** Without an initial NP-complete problem, we could never prove any problem NP-complete.
2. **It connects logic and computation.** The satisfiability of Boolean formulas captures the full power of non-deterministic polynomial-time computation.
3. **It shows the universality of SAT.** Every NP problem, no matter how different it looks (graphs, numbers, schedules), can be encoded as a SAT instance.

---

## 5.7 Summary

| Result | Significance |
|--------|-------------|
| SAT ∈ NP | Satisfying assignment is a polynomial-length certificate |
| Every NP language ≤_p SAT | NTM computations can be encoded as Boolean formulas |
| 3-SAT is NP-complete | Even restricting to 3 literals per clause stays hard |
| 2-SAT ∈ P | Restricting to 2 literals per clause makes it easy |

**Next:** [Chapter 6 — Classic NP-Complete Problems](06-classic-npc-problems.md)
