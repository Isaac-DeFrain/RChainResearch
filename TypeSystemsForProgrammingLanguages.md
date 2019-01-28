# Type Systems for Programming Languages

## Basic Types

### Intro
We begin with a simple language of arithmetic and logical expressions to illustrate the main features of the type theoretic approach to defining programming languages.

### Statics
The abstract syntax of `L^{Int, Bool}` is defined as follows:
```
  *Types*          T ::= Int | Bool
  *Expressions*    e ::= \bar{n} | true | false | e + e | e - e | e = e | if_t e then e else e fi
```

*Typing judgment* for `L^{Int, Bool}` has the form `e : t`

*Rules for deriving typing judgments*:
```
* {n}     : Int (for n \in \omega)

* true    : Bool

* false   : Bool

* e1:Int  , e2:Int => e1 + e2:Int

* e1:Int  , e2:Int => e1 - e2:Int

* e1:Int  , e2:Int => e1 = e2:Bool

* e1:Bool , e2:T , e3:T  => if_t e1 then e2 else e3 fi:T
```

These rules are said to be *syntax-directed* because at most one rule applies to any expression, and that rule is determined by the outermost form of that expression.

### Dynamics

#### Contextual Semantics
A *contextual semantics* is given by a set of *values*, a set of *evaluation contexts*, and a *primitive reduction relation*. Values are "fully evaluated" expressions. Evaluation contexts determine the order of evaluation of sub-expressions of a non-value expression. They are defined as follows:
```
  *Values*     
  *EvaluationContexts*   E ::= [] | E + e | v + E | E - e | v - E | E = e | v = E | if_t E then e1 else e2 fi
```

An *evaluation context* is an expression fragment with a designated "hole", `[]`. If `E` is an evaluation context and `e` is an expression, then `E[e]` is the expression obtained by "filling the hole" in `E` with the expression `e`, i.e. `E[e] := E[e / []]`.

The primitive reduction relation defines the primitive operations (primops) on values:
```
  {n1} + {n2} ~> {n1 + n2}
  {n1} - {n2} ~> {n1 - n2}
  {n1} = {n2} ~> true if n1 = n2, false otherwise
  if_t true  then e1 else e2 fi ~> e1
  if_t false then e1 else e2 fi ~> e2
```

An expression `e` such that `e ~> e'` for some `e'` is called a *redex*, in which case `e'` is called its *contractum*. Occasionally use the metavariable `r` to range over redices and `c` over their contracta.

The *one-step evaluation* relation `e |-> e'` is defined to hold iff `e = E[r]`, `e' = E[c]`, and `r ~> c`. The *multi-step evaluation* relation `e |->* e'` is the reflexive and transitive closure of the one-step evaluation relation. We say that the expression `e` *evaluates to* the value `v` iff `e |->* v`.

##### Lemma 1.1
1. If `v` is a value, then `v = E[e]` iff `E = []` and `e = v`.
2. If `v` is not a value, then there is at most one `E` such that `v = E[r]` and `r` is a redex.

##### Theorem 1.2 (Determinacy)

For any closed expression `e`, there is at most one value `v` such that `e |->* v`, i.e. `|->*` is a function.
