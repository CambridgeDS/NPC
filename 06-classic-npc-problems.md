# 6. Classic NP-Complete Problems

This chapter surveys the most important NP-complete problems and the reductions that prove them so. Each entry includes the formal problem statement, what the certificate is, and how the NP-completeness proof works.

---

## 6.1 The Karp 21

In his landmark 1972 paper, Richard Karp proved 21 problems NP-complete by a cascade of reductions from SAT. Here is the reduction tree:

```
                        SAT (Cook-Levin)
                         │
                     3-SAT
                    ╱    │     ╲
                  ╱      │       ╲
            3-COLOURING  │    INDEPENDENT SET
                     CLIQUE        │
                         │    VERTEX COVER
                         │         │
                    SUBSET SUM  SET COVER
                         │
                    PARTITION
                         │
                   3-PARTITION
                         │
                    BIN PACKING
                         │
                    KNAPSACK
```

*(Simplified — Karp's actual tree has more branches.)*

---

## 6.2 Problem Catalogue

### 3-SAT

| | |
|---|---|
| **Input** | Boolean formula φ in CNF with exactly 3 literals per clause |
| **Question** | Is φ satisfiable? |
| **Certificate** | A satisfying assignment |
| **Reduced from** | SAT (clause splitting, see Chapter 5) |

---

### CLIQUE

| | |
|---|---|
| **Input** | Graph G = (V, E), integer k |
| **Question** | Does G have a complete subgraph on ≥ k vertices? |
| **Certificate** | The k vertices |
| **Reduced from** | 3-SAT (see Chapter 4 worked example) |

---

### INDEPENDENT SET

| | |
|---|---|
| **Input** | Graph G = (V, E), integer k |
| **Question** | Does G have k pairwise non-adjacent vertices? |
| **Certificate** | The k vertices |
| **Reduced from** | CLIQUE (complement graph) |
| **Note** | S is independent in G ⟺ S is a clique in Ḡ |

---

### VERTEX COVER

| | |
|---|---|
| **Input** | Graph G = (V, E), integer k |
| **Question** | Is there a set S ⊆ V with |S| ≤ k such that every edge has at least one endpoint in S? |
| **Certificate** | The set S |
| **Reduced from** | INDEPENDENT SET |
| **Key fact** | S is a vertex cover ⟺ V \ S is an independent set |

---

### 3-COLOURING

| | |
|---|---|
| **Input** | Graph G = (V, E) |
| **Question** | Can the vertices be coloured with 3 colours so that no two adjacent vertices share a colour? |
| **Certificate** | The colouring function c: V → {1, 2, 3} |
| **Reduced from** | 3-SAT |
| **Note** | 2-colouring is in P (equivalent to checking bipartiteness) |

---

### HAMILTONIAN CYCLE

| | |
|---|---|
| **Input** | Graph G = (V, E) |
| **Question** | Does G contain a cycle that visits every vertex exactly once? |
| **Certificate** | The cycle (a permutation of vertices) |
| **Reduced from** | VERTEX COVER (via a gadget construction) |

---

### TRAVELLING SALESMAN (Decision)

| | |
|---|---|
| **Input** | Complete weighted graph G, budget B |
| **Question** | Is there a tour visiting all vertices with total weight ≤ B? |
| **Certificate** | The tour |
| **Reduced from** | HAMILTONIAN CYCLE (set weight 1 for edges in G, weight 2 otherwise, B = n) |

---

### SUBSET SUM

| | |
|---|---|
| **Input** | Integers a₁, ..., aₙ and target t |
| **Question** | Is there S ⊆ {1,...,n} with Σᵢ∈S aᵢ = t? |
| **Certificate** | The subset S |
| **Reduced from** | 3-SAT (using a clever number encoding of clauses) |
| **Note** | Pseudo-polynomial algorithm exists (dynamic programming in O(nt)) |

---

### PARTITION

| | |
|---|---|
| **Input** | Integers a₁, ..., aₙ |
| **Question** | Can {1,...,n} be split into S and S̄ with Σᵢ∈S aᵢ = Σᵢ∈S̄ aᵢ? |
| **Certificate** | The partition S |
| **Reduced from** | SUBSET SUM (set t = (Σ aᵢ)/2) |

---

### SET COVER

| | |
|---|---|
| **Input** | Universe U, collection of subsets S₁,...,Sₘ ⊆ U, integer k |
| **Question** | Can U be covered by ≤ k of the subsets? |
| **Certificate** | The k subsets |
| **Reduced from** | VERTEX COVER |

---

## 6.3 Strong vs Weak NP-Completeness

Some number problems like SUBSET SUM have *pseudo-polynomial* algorithms — algorithms polynomial in the numeric value of the input, but exponential in the number of bits.

> **Definition.** A problem is **strongly NP-complete** if it remains NP-complete even when all numbers in the input are bounded by a polynomial in the input size.

| Type | Example | Pseudo-poly algorithm? |
|------|---------|----------------------|
| Weakly NP-complete | Subset Sum, Partition, Knapsack | Yes (DP) |
| Strongly NP-complete | 3-SAT, Clique, 3-Colouring, 3-Partition | No (unless P = NP) |

---

## 6.4 Summary

NP-complete problems span many domains:
- **Logic:** SAT, 3-SAT
- **Graphs:** Clique, Independent Set, Vertex Cover, Colouring, Hamiltonian Cycle
- **Numbers:** Subset Sum, Partition, Bin Packing, Knapsack
- **Optimisation:** TSP, Set Cover
- **Scheduling, planning, and more...**

The key insight: despite looking very different, all these problems are computationally equivalent (under polynomial-time reductions). A polynomial-time algorithm for any one of them would give polynomial-time algorithms for all of them.

**Next:** [Chapter 7 — Implications and Coping Strategies](07-implications.md)
