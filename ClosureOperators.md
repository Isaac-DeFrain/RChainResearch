# Closure Operator

Let `S` be a set. A *closure operator* `cl` on `S` is a function `cl: P(S) -> P(S)` where `P(S)` is the *power* set of `S` satisfying the following properties:

1. Increasing: `X \subset Y  \implies  cl(X) \subset cl(Y)`
2. Extensive: `X \subset cl(X)`
3. Idempotent: `cl(cl(X)) = cl(X)`

where `X, Y \subset S`.

More generally, let `P = (S, \leq)` be a poset. A *closure operator* `cl` on `P` is a function `cl: P -> P` satisfying:

1. `x \leq y  \implies  cl(x) \leq cl(y)`
2. `x \leq cl(x)`
3. `cl(cl(x)) = cl(x)`

where `x, y \in P`

Viewing `P` as a category (with morphism a single morphism `x -> y` between objects `x` and `y` iff `x \leq y`), the closure operators are just the monads on `P`. The extensive, increasing, and idempotent properties of `cl` give:

1. shape:  `cl: P -> P` is a functor (hence an endofunctor)
2. wrap: `\eta: 1 -> cl`
3. roll:  `\mu: cl^2 -> cl`
