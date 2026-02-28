# 1. Turing Machines

## 1.1 Why Turing Machines?

Before we can say a problem is "hard," we need a precise model of computation. Turing machines (TMs) are the standard formal model because:

- They are simple enough to reason about mathematically.
- They are powerful enough to simulate any algorithm a real computer can run (Church-Turing thesis).
- Time and space usage on a TM can be measured precisely, giving us complexity classes.

---

## 1.2 Deterministic Turing Machine (DTM)

> **Definition.** A *deterministic Turing machine* is a 7-tuple
>
> M = (Q, Σ, Γ, δ, q₀, q_accept, q_reject)
>
> where:
> | Symbol | Meaning |
> |--------|---------|
> | Q | Finite set of states |
> | Σ | Input alphabet (does not contain the blank symbol ⊔) |
> | Γ | Tape alphabet, Σ ⊂ Γ, and ⊔ ∈ Γ |
> | δ | Transition function: Q × Γ → Q × Γ × {L, R} |
> | q₀ ∈ Q | Start state |
> | q_accept ∈ Q | Accept state |
> | q_reject ∈ Q | Reject state, q_reject ≠ q_accept |

### How it works

1. The input string w ∈ Σ* is written on an infinite tape, one symbol per cell, with blanks (⊔) filling the rest.
2. A read/write head starts at the leftmost symbol, in state q₀.
3. At each step the machine reads the symbol under the head, consults δ, then:
   - Writes a new symbol in that cell,
   - Moves the head one cell left (L) or right (R),
   - Transitions to a new state.
4. The machine **accepts** if it enters q_accept, **rejects** if it enters q_reject, and may **loop forever** otherwise.

### The language of a TM

> **Definition.** The *language recognised* (or *decided*) by M is
>
> L(M) = { w ∈ Σ* : M accepts w }
>
> We say M **decides** L(M) if M halts on every input (never loops).

### Running time

> **Definition.** Let M be a DTM that halts on all inputs. The *running time* of M is the function
>
> t_M(n) = max { number of steps M takes on input w : |w| = n }
>
> (worst-case over inputs of length n).

---

## 1.3 Non-Deterministic Turing Machine (NTM)

The key extension that gives us the class NP.

> **Definition.** A *non-deterministic Turing machine* is defined exactly like a DTM except the transition function becomes a **relation**:
>
> δ ⊆ (Q × Γ) × (Q × Γ × {L, R})
>
> Equivalently, δ: Q × Γ → P(Q × Γ × {L, R}), mapping each (state, symbol) pair to a **set** of possible (state, symbol, direction) triples.

### Computation tree

At each step an NTM may have multiple legal moves. This creates a **computation tree**:

```
              q₀
             / | \
           q₁  q₂  q₃      ← first non-deterministic branch
          / \   |   ...
        q₄  q₅  q₆
        ...
```

- Each root-to-leaf path is one possible computation.
- The NTM **accepts** w if **at least one** path reaches q_accept.
- The NTM **rejects** w if **every** path reaches q_reject (or halts without accepting).

### Running time of an NTM

> **Definition.** The running time of an NTM M is
>
> t_M(n) = max { length of the shortest accepting path on input w : w ∈ L(M), |w| = n }
>
> measured over the longest such shortest path across all accepted inputs of length n. For rejected inputs, all paths must halt, and we take the longest path.

More informally: t_M(n) is the depth of the computation tree on worst-case inputs of size n.

### Key intuition

An NTM can "guess" the right answer at each branch point. If there exists any sequence of correct guesses that leads to acceptance, the NTM accepts. This is the formal basis of the "guess and verify" view of NP.

---

## 1.4 Equivalence in Power, Not in Speed

> **Theorem.** Every language recognised by an NTM can also be recognised by a DTM.

*Proof sketch.* The DTM can simulate the NTM by systematically exploring all branches of the computation tree using breadth-first search. If the NTM accepts on some branch, the DTM will eventually find it. ∎

However, this simulation may take **exponentially** longer. If the NTM runs in time t(n) with branching factor b, the DTM simulation takes O(b^{t(n)}) steps. This exponential blowup is at the heart of the P vs NP question.

---

## 1.5 Decision Problems and Languages

In complexity theory we focus on **decision problems** — problems with a yes/no answer.

Every decision problem corresponds to a **language**:

> Given problem Π, define L_Π = { ⟨x⟩ : x is a yes-instance of Π }
>
> where ⟨x⟩ is a reasonable encoding of instance x as a binary string.

**Example.** The Hamiltonian Path problem:
- Instance: a graph G.
- Question: does G have a Hamiltonian path?
- Language: L_HAM = { ⟨G⟩ : G has a Hamiltonian path }.

We say a TM "solves" the decision problem if it decides the corresponding language.

---

## 1.6 Summary

| Concept | Key Point |
|---------|-----------|
| DTM | One move per step; deterministic |
| NTM | Multiple possible moves; accepts if *any* branch accepts |
| Power | DTM and NTM recognise the same languages |
| Speed | NTM may be exponentially faster (we don't know if this gap is inherent) |
| Decision problem ↔ Language | Every yes/no problem is a set of strings |

**Next:** [Chapter 2 — Complexity Classes](02-complexity-classes.md)
