# Nominal Logic - Andrew M. Pitts

## Introduction
Abstract away from details of concrete syntax in terms of stings of symbols and instead work solely with parse trees - 'abstract syntax' of the language. This grants access to two extremely useful and inter-related tools:

1. Definition by recursion on the structure of parse trees.

2. Proof by induction on that structure.

* `'a`-equivalence classes of parse trees

However, we say that we will quotient the collection of parse trees by a suitable equivalence relation of `'a`-conversion, identifying trees up to renaming of bound variables; but then we try to make the use of `'a`-equivalence classes *as implicit as possible* by dealing with them via suitably chosen representatives.

* No choosing suitable representatives!

'Barendregt Variable Convention': chooses representative parse tree whose bound variables are *fresh*, i.e. mutually distinct and distinct from any (free) variables in the current context.

* `'a`-conversion, freshness, variable-binding, ... can all be defined purely in terms of the operation of **swapping** pairs of names
  * Freshness of a name for an object is expressed in terms of the name not being in some finite set of names that **supports** the object, i.e. swapping pairs of names not in the set leaves the object unchanged
  * Notion of *supports* is weak second order: existential quantification over finite sets of names

Wanted: to use structural recusion for defining functions on parse trees and structural induction for proving properties of them.

Nominal Logic: first-order theory of names, swapping, and freshness.


## Equivariant Predicates
The fundamental assumption underlying Nominal Logic is that *the only predicates* (when describing properties of syntax) *we ever deal with are equivariant ones, in the sense that their validity in invariant under swapping* (i.e. transposing, or interchanging) *names*.

Names of what? Name of entities that may be subject to binding by some of the syntactical constructions under consideration. In nominal logic, these sorts of names, the ones that may be subjected to swapping, are called *atoms* - the terminology refers back to the origins of theory in the Fraenkel-Mostowski permutation model of set theory. Atoms have quite differen logical properties from *constants* (in the usual sense of first-order logic), which being constant are not subjected to swapping.

> The distinction between atom and constant has to do with the issue of binding, rather than substitution. 

A syntactic category of *variables*, by which is usually meant entities that may be subject to substitution, might be represented in nominal logic by atoms or by constants, depending upon circumstances: constants will do in a situation where variables are never bound, but can be substituted; otherwise we should use atoms. Interestingly, we can make this distinction between 'bindable' names and names of constants entirely in terms of properties of swapping names, prior to any discussion of substitution and its properties.

Emphasis on *swapping* two names, rather than on the apparently more primitive notion of *renaming* one name by another because the swapping operation is idempotent: a swap followed by the same swap is equivalent to doing nothing. As a consequence, the class of equivariant predicates, i.e. , has excellent logical properties; it contains the equality predicate and is closed under negation, conjugation, disjunction, existential and universal quantification, formation of least and greatest fixed points of monotone operators, etc. The same is not true for renaming. (E.g. the validity of a negated eqaulity between atoms is not necessarily preserved under renaming.)

One of the main messages of this paper:

> We should take equivariance into account when we reason about syntactical structures.

Take note of the fact that:

> Name swapping and equivariance property provide a simple and useful foundation for discussing properties of names and binding in syntax.

E.g. a simple example from type theory:






































