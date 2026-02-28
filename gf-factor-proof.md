# Proof: A Third (g,f)-Factor with Distinct Degree Pattern Must Exist

## Problem Statement

Let G be a graph, and let each node i have integer bounds (gᵢ, fᵢ) specifying the minimum and maximum allowable degree. A **(g,f)-factor** of G is a subgraph in which every node i has degree d satisfying gᵢ ≤ d ≤ fᵢ.

Suppose two valid (g,f)-factors G₀ and G₁ exist, and three designated nodes X, Y, Z satisfy:

- In G₀: deg(X) = 0, deg(Y) = 0, deg(Z) = 0
- In G₁: deg(X) = 1, deg(Y) = 1, deg(Z) = 1

**Prove** that there exists at least one other valid (g,f)-factor G₂ in which the degree triple (deg(X), deg(Y), deg(Z)) is neither (0,0,0) nor (1,1,1).

---

## Proof

### Step 1 — Symmetric difference with two-colouring

Define the **symmetric difference**

D = E(G₀) △ E(G₁)

and colour each edge:

| Colour | Meaning |
|--------|---------|
| **Red** | Edge in G₁ \ G₀ (present in G₁ but not G₀) |
| **Blue** | Edge in G₀ \ G₁ (present in G₀ but not G₁) |

For every vertex v, write r(v) for the number of red edges and b(v) for the number of blue edges incident to v in D. Then:

> r(v) − b(v) = deg_{G₁}(v) − deg_{G₀}(v)

For X, Y, Z in particular, since deg_{G₀} = 0 and deg_{G₁} = 1:

> r(v) = 1, b(v) = 0, for each v ∈ {X, Y, Z}

Each of these three vertices is incident to **exactly one edge in D, and it is red**.

---

### Step 2 — Decompose D into alternating paths and cycles

At each vertex v of D, pair up red and blue edges arbitrarily: form min(r(v), b(v)) red–blue pairs. The |r(v) − b(v)| unpaired edges (all the same colour) remain.

Following these pairings traces out edge-disjoint **alternating trails** — trails where consecutive edges alternate between red and blue. Each trail is either:

- an **alternating cycle**, or
- an **alternating path** whose two endpoints are vertices with r(v) ≠ b(v).

Since r(v) = 1 and b(v) = 0 for each of X, Y, Z, all three are **endpoints of alternating paths** in this decomposition.

---

### Step 3 — Pigeonhole: not all three can share one path

Each alternating path has **exactly two endpoints**. Three vertices X, Y, Z therefore require **at least two distinct paths** (since a single path accommodates only two endpoints).

Consequently, at least one of X, Y, Z lies on a path that does **not** contain the other two. Without loss of generality, assume vertex X is the endpoint of a path Pₓ that does not contain both Y and Z.

---

### Step 4 — Flipping an alternating path preserves feasibility

> **Lemma.** For any alternating path (or cycle) P in D, the subgraph
>
> G₂ = G₀ △ P
>
> (add every red edge of P to G₀; remove every blue edge of P from G₀) is a valid (g,f)-factor.

**Proof of Lemma.**

| Vertex type | Degree change | Why it stays feasible |
|-------------|---------------|-----------------------|
| **Not on P** | 0 | Unaffected; still valid since G₀ was valid |
| **Internal vertex of P** | +1 (red) − 1 (blue) = 0 | Alternation guarantees one red and one blue edge at every internal vertex; degree unchanged |
| **Endpoint with red terminal edge** | +1 | This vertex has r(v) > b(v), so deg_{G₁}(v) ≥ deg_{G₀}(v) + 1, giving deg_{G₂}(v) = deg_{G₀}(v) + 1 ≤ deg_{G₁}(v) ≤ fᵥ. Also gᵥ ≤ deg_{G₀}(v) < deg_{G₂}(v). ✓ |
| **Endpoint with blue terminal edge** | −1 | This vertex has b(v) > r(v), so deg_{G₁}(v) ≤ deg_{G₀}(v) − 1, giving deg_{G₂}(v) = deg_{G₀}(v) − 1 ≥ deg_{G₁}(v) ≥ gᵥ. Also deg_{G₂}(v) < deg_{G₀}(v) ≤ fᵥ. ✓ |

In every case the degree remains within [gᵥ, fᵥ]. ∎

---

### Step 5 — Construct G₂ and verify the degree pattern

Set **G₂ = G₀ △ Pₓ**. By the Lemma, G₂ is a valid (g,f)-factor.

Since X is a red endpoint of Pₓ:

> deg_{G₂}(X) = deg_{G₀}(X) + 1 = **1**

Two sub-cases arise for the other endpoint of Pₓ:

#### Sub-case (a): Pₓ contains neither Y nor Z

Y and Z are not on Pₓ, so their degrees are unchanged from G₀:

> **(deg(X), deg(Y), deg(Z)) = (1, 0, 0)**

This is neither (0,0,0) nor (1,1,1). ✓

#### Sub-case (b): Pₓ contains exactly one of Y or Z (say Y)

Y has degree 1 in D and therefore can only appear as the **other endpoint** of Pₓ (not as an internal vertex, since internal vertices need degree ≥ 2 on the path). Since r(Y) = 1 and b(Y) = 0, vertex Y is a red endpoint, so:

> deg_{G₂}(Y) = deg_{G₀}(Y) + 1 = **1**

Meanwhile Z is not on Pₓ, so:

> **(deg(X), deg(Y), deg(Z)) = (1, 1, 0)**

This is neither (0,0,0) nor (1,1,1). ✓

---

### Conclusion

In every case, flipping the alternating path Pₓ produces a valid (g,f)-factor G₂ whose degree pattern on {X, Y, Z} differs from both (0,0,0) and (1,1,1).  **∎**

---

## Remark

The proof generalises naturally. The core mechanism is:

1. The symmetric difference of two (g,f)-factors decomposes into alternating structures.
2. Flipping any single alternating path/cycle yields another valid factor.
3. Three odd-degree vertices cannot all be paired on a single path, so at least one flip "decouples" a vertex from the others.

This is closely related to the theory of **T-joins** and the structure of factor polytopes in combinatorial optimisation.
