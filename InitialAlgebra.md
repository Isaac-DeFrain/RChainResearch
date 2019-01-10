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

E.g. abelian groups are `F`-algebras for the same functor `F(G) = 1 + G + G*G` as for groups with an additional axiom for commutativity: `m o t = m`, where `m` is multiplication and `t(g,h) = (h,g)` is the transpose on `G*G`.












