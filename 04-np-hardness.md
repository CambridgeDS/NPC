# 4. NP-Hardness and NP-Completeness

This chapter gives the precise formal definitions — the heart of the theory.

---

## 4.1 NP-Hard

> **Definition.** A language H is **NP-hard** if for every language L ∈ NP:
>
> L ≤_p H
>
> In words: every problem in NP can be polynomial-time reduced to H.

### Key points about NP-hardness

- An NP-hard problem is **at least as hard as every problem in NP**.
- An NP-hard problem **need not be in NP itself**. It can be harder — even undecidable.
- If any NP-hard problem has a polynomial-time algorithm, then **P = NP** (because every NP problem reduces to it in poly time).

### Examples of NP-hard problems NOT in NP

| Problem | Why it's not in NP |
|---------|--------------------|
| Halting problem | Undecidable — not even in EXP |
| QSAT (quantified Boolean formula) | PSPACE-complete; not known to be in NP |
| Optimal TSP tour length (function version) | Not a decision problem |

---

## 4.2 NP-Complete

> **Definition.** A language L is **NP-complete** if:
>
> 1. L ∈ NP, **and**
> 2. L is NP-hard (i.e., ∀ A ∈ NP, A ≤_p L).

NP-complete problems are the **hardest problems in NP** — they sit at the boundary.

```
┌──────────────────────────────────────────────────────┐
│                     NP-hard                          │
│                                                      │
│   Halting Problem, QSAT, ...                         │
│                                                      │
│   ┌──────────────────────────────────────────────┐   │
│   │              NP-complete                     │   │
│   │                                              │   │
│   │   SAT, 3-SAT, CLIQUE, VERTEX COVER,         │   │
│   │   HAM-CYCLE, SUBSET-SUM, 3-COLOURING, ...   │   │
│   │                                              │   │
│   │       ┌──────────────────────────────┐       │   │
│   │       │            P                 │       │   │
│   │       │                              │       │   │
│   │       │  (if P ≠ NP, this is         │       │   │
│   │       │   strictly inside NPC)       │       │   │
│   │       └──────────────────────────────┘       │   │
│   │                                              │   │
│   └──────────── in NP ───────────────────────────┘   │
│                                                      │
└──────────────────────────────────────────────────────┘
```

---

## 4.3 How to Prove a Problem is NP-Complete

To show a new problem B is NP-complete, you must show two things:

### Step 1: B ∈ NP

Show that a solution (certificate) for B can be **verified** in polynomial time. Typically:
- Describe what the certificate is.
- Describe the verification algorithm.
- Argue it runs in polynomial time.

### Step 2: B is NP-hard

Show that some **known** NP-complete problem A reduces to B:

> A ≤_p B

Since A is NP-complete, every NP problem reduces to A, and by transitivity, every NP problem reduces to B.

**Note:** For Step 2 you need at least one "seed" NP-complete problem to start from. This seed is SAT, proved NP-complete by the Cook-Levin theorem (Chapter 5).

---

## 4.4 Worked Example: CLIQUE is NP-Complete

**CLIQUE:** Given graph G = (V, E) and integer k, does G contain a complete subgraph on k vertices?

### Step 1: CLIQUE ∈ NP

- **Certificate:** A set S ⊆ V with |S| = k.
- **Verification:** Check |S| = k and that for all u, v ∈ S with u ≠ v, {u,v} ∈ E.
- **Time:** O(k²) ⊆ O(n²). ✓

### Step 2: 3-SAT ≤_p CLIQUE

Given a 3-SAT formula φ with m clauses C₁, ..., C_m:

**Construction:** Build graph G = (V, E):
- For each literal ℓ in clause Cᵢ, create a vertex vᵢ,ℓ. So |V| = 3m.
- Add edge {vᵢ,ℓ , vⱼ,ℓ'} if and only if:
  - i ≠ j (they are from different clauses), AND
  - ℓ and ℓ' are not complementary (ℓ ≠ ¬ℓ').
- Set k = m.

**Correctness (⟹):** If φ is satisfiable, pick one true literal per clause. The corresponding m vertices form a clique (they are from distinct clauses and are mutually consistent, so all edges exist).

**Correctness (⟸):** If G has a clique S of size m, then S contains one vertex from each clause (since no two vertices from the same clause are connected). Setting those literals to true satisfies φ (they are mutually consistent since complementary literals are never both in S).

**Efficiency:** The construction is O(m²). ✓

---

## 4.5 The Structure of NP-Completeness

> **Theorem (Ladner, 1975).** If P ≠ NP, then there exist languages in NP that are neither in P nor NP-complete. These are called **NP-intermediate** problems.

Candidate NP-intermediate problems (not known to be in P or NP-complete):
- **Graph isomorphism**
- **Factoring** (the decision version)
- **Discrete logarithm**

---

## 4.6 Formal Summary

| Class | Definition | Intuition |
|-------|-----------|-----------|
| **NP-hard** | ∀ L ∈ NP: L ≤_p H | At least as hard as everything in NP |
| **NP-complete** | NP-hard AND in NP | The hardest problems within NP |
| **NP-intermediate** | In NP, not in P, not NP-complete | Exists if P ≠ NP (Ladner's theorem) |

### The fundamental equivalences

The following are all equivalent (any one implies all the others):

1. Some NP-complete problem is in P.
2. Every NP-complete problem is in P.
3. P = NP.

**Next:** [Chapter 5 — Cook's Theorem](05-cooks-theorem.md)
