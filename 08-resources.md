# 8. Additional Resources

A curated list of video lectures, online courses, textbooks, and references for going deeper into NP-completeness and computational complexity theory.

---

## Video Lectures (YouTube)

### Beginner-Friendly

| Resource | Description |
|----------|-------------|
| [P vs NP and the Computational Complexity Zoo](https://www.youtube.com/watch?v=YX40hbAHx3s) (hackerdashery) | Excellent animated 10-minute explainer. The best starting point if you've never seen P vs NP before. |
| [Abdul Bari — NP-Hard and NP-Complete](https://www.youtube.com/playlist?list=PLDN4rrl48XKpZkf03iYFl-O29szjTrs_O) (Algorithms playlist) | Clear, visual explanations of NP-hard, NP-complete, reductions, Cook's theorem. Part of a larger algorithms playlist. |
| [P, NP, NP-Hard and NP-Complete Problems](https://www.youtube.com/watch?v=XOna_Xpi8ZI) | Concise overview distinguishing P, NP, NP-hard, NP-complete with examples like TSP and Knapsack. |

### University Lectures

| Resource | Description |
|----------|-------------|
| [MIT 6.046J — Lecture 16: Complexity, P, NP, NP-completeness, Reductions](https://ocw.mit.edu/courses/6-046j-design-and-analysis-of-algorithms-spring-2015/resources/lecture-16-complexity-p-np-np-completeness-reductions/) (Prof. Erik Demaine) | Rigorous MIT lecture covering P vs NP, reductions, and NP-completeness proofs for 3-SAT, Subset Sum, and more. |
| [MIT 18.404J — Theory of Computation](https://ocw.mit.edu/courses/18-404j-theory-of-computation-fall-2020/) (Prof. Michael Sipser) | Full MIT course by the author of the standard textbook. Covers automata, computability, and complexity. Video lectures available. |
| [Ryan O'Donnell — CMU Complexity Theory](https://www.youtube.com/playlist?list=PLm3J0oaFUx28amYIFQS18p_GHKfUYmKN-) | CMU undergraduate + graduate complexity lectures. The most comprehensive free video series on the subject. |
| [Harry Porter — Theory of Computation](https://www.youtube.com/playlist?list=PLbtzT1TYeoMjNOGEiaRmm_vMIwUAhiP9d) | Portland State lectures covering finite automata through Turing machines and complexity classes. |

---

## Online Courses

| Course | Platform | Level | Notes |
|--------|----------|-------|-------|
| [Algorithms Specialization](https://www.coursera.org/specializations/algorithms) (Tim Roughgarden, Stanford) | Coursera | Intermediate | Course 4 specifically covers [NP-Complete Problems and What To Do About Them](https://www.coursera.org/learn/algorithms-npcomplete). One of the highest-rated algorithm courses online. |
| [Theory of Computation](https://ocw.mit.edu/courses/18-404j-theory-of-computation-fall-2020/) (Michael Sipser, MIT) | MIT OCW | Intermediate | Free. Full video lectures + assignments. Covers Turing machines, decidability, and complexity. |
| [Computational Complexity](https://nptel.ac.in/courses/106104220) | NPTEL (IIT) | Advanced | Indian Institute of Technology lectures, freely available. Covers P, NP, polynomial hierarchy, circuit complexity. |
| [Automata, Computability, and Complexity](https://ocw.mit.edu/courses/6-045j-automata-computability-and-complexity-spring-2011/) (Scott Aaronson, MIT) | MIT OCW | Intermediate | Another excellent MIT offering with a different flavour. |

---

## Textbooks (with free drafts)

| Book | Authors | Free? | Best for |
|------|---------|-------|----------|
| [Computational Complexity: A Modern Approach](https://theory.cs.princeton.edu/complexity/) | Sanjeev Arora & Boaz Barak | [Free draft PDF](https://theory.cs.princeton.edu/complexity/book.pdf) | The comprehensive graduate reference. Covers everything from P vs NP to PCP theorem, derandomisation, quantum computing. |
| *Introduction to the Theory of Computation* | Michael Sipser | No (textbook) | The standard undergraduate text. Part 3 covers complexity. Exceptionally clear writing with "proof idea" sections. |
| *Computers and Intractability: A Guide to the Theory of NP-Completeness* | Michael Garey & David Johnson | No (textbook) | The classic NP-completeness reference. Contains a catalogue of hundreds of NP-complete problems. |
| *Algorithm Design* | Jon Kleinberg & Eva Tardos | No (textbook) | Chapters 8 (NP and computational intractability) is an excellent practical introduction. |
| [Algorithms Illuminated, Part 4](https://www.algorithmsilluminated.org/) | Tim Roughgarden | Partial | Companion to the Coursera specialization. Covers NP-completeness and coping strategies. |

---

## Seminal Papers

| Paper | Year | Significance |
|-------|------|-------------|
| [The Complexity of Theorem-Proving Procedures](https://doi.org/10.1145/800157.805047) — Stephen Cook | 1971 | Proves SAT is NP-complete (Cook's theorem). |
| [Reducibility Among Combinatorial Problems](https://doi.org/10.1007/978-1-4684-2001-2_9) — Richard Karp | 1972 | Proves 21 problems NP-complete via reductions from SAT. |
| [The Knowledge Complexity of Interactive Proof Systems](https://doi.org/10.1137/0217018) — Goldwasser, Micali, Rackoff | 1989 | Introduces zero-knowledge proofs, connecting NP to cryptography. |
| [On the Computational Complexity of Algorithms](https://doi.org/10.1090/S0002-9947-1965-0170805-7) — Juris Hartmanis & Richard Stearns | 1965 | Founds computational complexity theory; proves the time hierarchy theorem. |

---

## Quick References and Wikis

| Resource | Description |
|----------|-------------|
| [Complexity Zoo](https://complexityzoo.net/) | Encyclopedia of complexity classes — over 500 classes with definitions and relationships. |
| [GeeksforGeeks — P, NP, CoNP, NP-hard and NP-complete](https://www.geeksforgeeks.org/dsa/types-of-complexity-classes-p-np-conp-np-hard-and-np-complete/) | Quick refresher with diagrams and examples. |
| [Brilliant.org — Computational Complexity](https://brilliant.org/wiki/computational-complexity/) | Interactive wiki with problems to solve. |
| [Wikipedia — NP-completeness](https://en.wikipedia.org/wiki/NP-completeness) | Surprisingly thorough and well-referenced. |
| [NP-Complete — A Rough Guide](https://www.mathsisfun.com/sets/np-complete.html) (Math is Fun) | Very gentle non-technical introduction. |

---

## Suggested Learning Paths

### Path 1: Quick Overview (1-2 hours)
1. Watch the [hackerdashery P vs NP video](https://www.youtube.com/watch?v=YX40hbAHx3s)
2. Read through this tutorial (Chapters 1-7)
3. Browse [GeeksforGeeks quick reference](https://www.geeksforgeeks.org/dsa/types-of-complexity-classes-p-np-conp-np-hard-and-np-complete/)

### Path 2: Solid Understanding (1-2 weeks)
1. This tutorial (Chapters 1-7)
2. Sipser's textbook, Part 3 (Chapters 7-9)
3. MIT 18.404J lectures on complexity (weeks 8-12)

### Path 3: Deep Dive (1 semester)
1. Arora & Barak [free draft](https://theory.cs.princeton.edu/complexity/book.pdf), Chapters 1-6
2. Tim Roughgarden's [Coursera specialization](https://www.coursera.org/specializations/algorithms) (Course 4)
3. Ryan O'Donnell's [CMU lectures](https://www.youtube.com/playlist?list=PLm3J0oaFUx28amYIFQS18p_GHKfUYmKN-)
4. Read the Cook (1971) and Karp (1972) original papers
