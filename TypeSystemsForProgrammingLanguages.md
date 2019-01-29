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
*   {n} : Int   (for n \in \omega)

*  true : Bool

* false : Bool

* e1:Int  /\ e2:Int -> e1 + e2:Int

* e1:Int  /\ e2:Int -> e1 - e2:Int

* e1:Int  /\ e2:Int -> e1 = e2:Bool

* e1:Bool /\ e2:T /\ e3:T  -> if_t e1 then e2 else e3 fi:T
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
                    {n1} = {n2} ~> true (n1 = n2), false (otherwise)
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

#### Evaluation Semantics
```
                                                        {n} => {n}
                                                       true => true
                                                      false => false
                     e1 => {n1}  /\ e2 => {n2}  ==> e1 + e2 => {n1 + n2}
                                  .             ==> e1 - e2 => {n1 - n2}
                                  .             ==> e1 = e2 => true  (n1 = n2)
                                  .             ==>    .    => false (n1 =/= n2)
      e1 => true /\ e2 => v  ==> if_t e1 then e2 else e3 fi => v
     e1 => false /\ e3 => v  ==> if_t e1 then e2 else e3 fi => v
```

##### Theorem 1.4 (Determinacy):
For every closed expression `e` there is at most one `v` such that `e => v`.

> The evaluation semantics is equivalent to the contextual semantics in the sense that `e => v  <->  e |->* v`.
>
>Proof:
>
>1. The relation `e |->* v` is closed under the defining conditions of the `=>` relation, the smallest such relation. Thus `e => v  ->  e |->* v`.
>2. The `=>` relation is closed under "head expansion", i.e. if `e => v /\ e' |-> e  ->  e' => v`.
>3. `e |->* v  ->  e => v`

##### Facts about Contextual Semantics
1. If `e1 + e2 |->* v`, then `e1 |-> v1` and `e2 |-> v2` for some values `v1`, `v2`. (A similar property holds for the other primitive operations of `L^{Int, Bool}`)
2. If `if_t e then e1 else e2 fi |->* v`, then `e |->* v'` for some value `v'`.

### Type Soundness

##### Lemma 1.7 (Replacement):
````
  E[e] : t  ==>  \exists t_e (e : t_e /\ \forall e' ( e' : t_e /\ E[e'] : t ) )
```

##### Lemma 1.8 (Subject Reduction):
```
  e ~> e' /\ e : t  ==>  e' : t
```

##### Lemma 1.9 (Preservation):
```
  e |-> e' /\ e : t  ==>  e' : t
```

##### Lemma 1.10 (Canonical Forms):
```
  v : Int   ==>  \exists n (v = {n})
  v : Bool  ==>  true \xor false
```
##### Theorem 1.11 (Progress):
If `e : t`, then either `e` is a value, or `\there e' (e |-> e')`

##### Type Soundness in Evaluation Semantics
We begin be introducing the notion of an *answer* which is the ultimate result of evaluation.
```
  *Answers*     a ::= Ok(v) | Wrong
```

Define `a : t` iff `a = Ok(v)` and `v : t`. Thus `Wrong` is ill-typed.


## Function and Product Types
We consider the language `L^{1, /times, ->}` with product and function types.

### Statics
The abstract syntax of `L^{1, \times, ->}` is given by the following grammar
```
  *Types*         t ::= Unit | t1 \times t2 | t1 -> t2
  *Expressions*   e ::= x | <e1,e2>_{t1,t2} | proj1_{t1,t2}(e) | proj2_{t1,t2}(e) | fun(x:t1):t2 in e | app_{t1,t2}(e1,e2)
```

In the expression `fun(x:t1):t2 in e` the variable `x` is bound in `e`.
