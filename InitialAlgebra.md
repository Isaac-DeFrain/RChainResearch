# Initial Algebra

An **initial algebra** is an *initial object* in the category of `F`-algebras for a given endofunctor `F`. This initially provides a general framework for induction and recursion.

E.g. consider the endofunctor `1+(-)` on the categorey of sets, where `1` is the one-point (singleton) set, the *terminal object* in the category. An algebra for this endofunctor is a set `X` (called the *carrier*) of the algebra) together with a point `x \in X` and a function `X -> X`. The set of natural numbers is the carrier of the initial such algebra: the point is `zero` and the funcion is the successor map.

E.g. consider the endofunctor `1+\mathbb{N}*(-)` on the category of sets, where `\mathbb{N}` is the set of natural numbers. An algebra for this endofunctor is a set `X` together with a point `x \in X` and a function `\mathbb{N}*X -> X`. The set of finite lists of natural numbers is the initial such algebra; point is the empty list and function is *cons*, taking a number and a finite list, and returning a new finite list with the number at the head and the original list as the tail.

## F-algebras
*F-algebras* generalize algebraic structure. Rewriting the algebraic laws in terms of morphisms eliminates all references to quantified elements from the axioms, and these algebraic laws may then be glued together in terms of a single functor `F`, called the *signature*.

`F`-algebras can be used to represent data structures used in programming, such as lists and trees.

* Main related concepts:
  * Initial `F`-algebras may serve to encapsulate the *induction principle*
  * The dual construction, `F`-coalgebras

************
*** Def: ***
************
If `C` is a category, and `F: C -> C` is an endofunctor of `C`, then an **`F`-algebra** is a tuple `(A,'a)`, where `A \in C` is an object of `C` and `'a \in Hom(C)` is a `C`-morphism with `F(A) -> A`. The object `A` is called the *carrier* of the algebra. Algebras are often referred to by their carrier instead of the tuple.

A **homomorphism** from an `F`-algebra `(A, 'a)` to an `F`-algebra `(B, 'b)` is a `C`-morphism `f: A -> B` such that `f o 'a = 'b o F(f)`, according to the following commuting diagram:
```
				       'a
				F(A) ------> A
				  |          |
				  |          |
			      F(f)|          |f
				  |          |
				  v    'b    v
				F(B) ------> B
```

Equipped with homomorphisms as the morphisms, `F`-algebras constitute a category.

The dual construction are `F`-coalgebras, which are objects `A*` together with a morphism `'a*: A* -> F(A*)`.


#### Algebraic Structures

> Most structures are `F`-algebras.

Examples
* *Abelian groups* are `F`-algebras for the same signature `F(G) = 1 + G + G*G` as for groups with an additional axiom for commutativity: `m o t = m`, where `m` is multiplication and `t(g,h) = (h,g)` is the transpose on `G*G`

* *Monoids*, which generalize groups in that the monoid element does not need to have an inverse, are `F`-algebras of signature `F(M) = 1 + M*M`

* *Semigroups* are `F`-algebras of signature `F(S) = S*S`

* *Rings*, *domains*, and *fields* are also `F`-algebras with signature involving two laws `+,o: R*R -> R`, an additive `0: 1 -> R`, a multiplicative identity `1: 1 -> R`, and an additive inverse for each element `-: R -> R`. Since all these functions share the same codomain `R`, they can be glued into a single signature function `1 + 1 + R + R*R + R*R -> R`, with axioms to express associativity, distributivity, etc. This makes rings `F`-algebras on the category of sets with signature `1 + 1 + R + R*R + R*R`.

* When it comes vector *spaces* and *modules*, the signature functor includes a *scalar multiplication* `k*E -> E`, and the signature `F(E) = 1 + E + k*E` is parameterized by `k` over the category of fields or rings

* *Algebras over a field* can be viewed as `F`-algebras of signature `1 + 1 + A + A*A + A*A + k*A` over the category of sets, of signature `1 + A*A` over the category of modules (a module with an internal multiplication), and of signature `k*A` over the category of rings (a ring with a scalar multiplication, e.g. a function space), when they associative and unitary.

##### Recurrence
COnsider the functor `F: Set -> Set` that sends a set `X` to `1 + X`. Here, `Set` denotes the category of sets, `+` denotes the usual *coproduct* given by *disjoint union*, and `1` is a terminal object (i.e. a singleton set). Then the set `\mathbb{N}` of natural numbers together with the function `[zero,succ]: 1 + \mathbb{N} -> \mathbb{N}`, i.e. the coproduct of the functions `zero: 1 -> \mathbb{N}` (whose image is `0`) and `succ: \mathbb{N} -> \mathbb{N}` (which sends an integer `n` to `n + 1`), is an `F`-algebra.

### Initial `F`-algebra
If the category of `F`-algebras for a given endofunctor `F` has an initial object, it is called the *initial algebra*. The algebra `(\mathbb{N}, [zero,succ])` is an initial algebra.

Types defined by using the *least fixed point* construct with functor `F` can be regarded as an initial `F`-algebra, provided that parametricity holds for the type.


### Terminal `F`-coalgebra
In a dual way, a similar relationship exists between the notions of *greatest fixed point* and terminal `F`-coalgebra, these can be used for allowing *potentially infinite* objects while maintaining a strong normalization property. In the strongly normalizing Charity programming language (i.e. each program in it terminates), *coinductive* data types can be used to achieve surprising results, e.g. defining lookup constructs to implement such "strong" functions like the Ackermann function.


## Final Coalgebra
Dually, a **final coalgebra** is a *terminal object* in the category of `F`-coalgebras. The finality provides a good framework for *coinduction* and *corecursion*.


## Theorems
















