# Bisimulation

Bisimulation is a *binary relation* between *state transition systems*, associating systems that behave in the same way in the sense that one system simulates the other and vice versa.

Intuitively, two systems are bisimilar if they match each other's moves. In this sense, each of these systems cannot be distinguished from the other by an observer.

## Formal Definition
Given a labeled transition system `(S, L, ->)`, a *bisimulation* relation is a binary relation `R` over `S` (i.e. `R \subset S x S`) such that `R` and its converse `R^T` are *simulations*.

Equivalently, `R` is a bisimulation if for every pair of elements `p`,`q` in `S` with `(p,q) \in R`, for all `a \in L`:
* for all `p' \in S`, `a: p -> p'` implies that there is a `q' \in S` such that `a: q -> q'` and `(p',q') \in R`; and
* symetrically, for all `q' \in S`, `a: q -> q'` implies that there is a `p' \in S` such that `a: p -> p'` and `(p',q') \in R`.

Given two states `p` and `q` in `S`, `p` is **bisimilar** to `q`, written `p ~ q` if there exists a bismulation `R` such that `(p,q) \in R`.

The bisimilarity relation `~` is an equivalence relation and the largest bismiulation relation over a given transition system.

### Relational Definition
Bisimulation can be defined in terms of composition of relations as follows:

Given a labeled transition system `(S, L, ->)`, a *bisimulation* relation is a binary relation `R` over `S` (i.e. `R \subset S x S`) such that for all `a \in L`:
```
    R ; ->^a \subset ->^a ; R   and   R^{-1} ; ->^a \subset ->^a ; R^{-1}
```

From monotonicity and continuity of relation composition, it follows that the set of bisimulations is closed under unions (joins in the poset of relations), and a simple algebraic calculation shows that the relation of bisimilarity - the join of all bisimualtions - is an equivalence relation.

### Fixed Point Definition
Given a labeled transition system `(S, L, ->)`, we define a function `F: P(S x S) -> P(S x S)` from binary relations over `S` to binary relations over `S`, as follows:

Let `R` be a binary relation over `S`. `F(R)` is defined to be the set of all pairs `(p,q) \in S x S` such that:
* `\forall a \in L. \forall p' \in S. a: p -> p'` implies `\exists q' \in S. a: q -> q' /\ (p',q') \in R`; and
* `\forall a \in L. \forall q' \in S. a: q -> q'` implies `\exists p' \in S. a: p -> p' /\ (p',q') \in R`.

Bisimilarity is then defined as the greatest fixed point of the function `F`.

### Game-Theoretic Definition

### Coalgebraic Definition
