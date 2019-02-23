# Namespace Logic for Rho-Calculus Notes

### Abstract
In [A Reflective High-Order Calculus]() it was observed that a theory like the `pi`-calculus, dependent on a theory of *names*, can be *closed*, through a mechanism of *quoting*, so that *quoted processes* provide the necessary notion of names. We expand on this theme by examining a Hennessey-Milner (HM) logic corresponding to an asynchronous message-passing calculus built on a notion of quoting. Like standard HM logics, the logic exhibits formulae corresponding to sets of processes, but a new class of formulae, corresponding to sets of names, also emerges. This feature provides for a number of interesting possible applications from security to data manipulation. Specifically, we illustrate formulae for controlling process response on ranges of names reminiscent  of a (static) constraint on port access in a firewall configuration. Likewise, we exhibit formulae in a names-as-data paradigm corresponding to validation for fragment of `XML Schema`.

## Introduction
Practically, whether we consider MAC/IP addresses, domain names, or URL's, it is clear that distributed computing is practiced, today, using names.

Theoretically, nowhere in the tools available to the computer scientist is there a countably infinite set of *atomic* entities that might function as names. All such sets, e.g. the natural numbers, the set of strings of finite length on some alphabet, etc., are *generated* from a finite presentation, and as such the elements of these sets inherit *structure* from the generating procedure. This structure can be "forgotten", but comes to the fore when building *executable* models of these calculi.

The fact that the [`pi`-calculus](http://www.lfcs.inf.ed.ac.uk/reports/91/ECS-LFCS-91-180/) is not a closed theory, but rather a theory dependent upon some theory of names is both enabling and limiting. Biztalk: tcp/ip ports, urls, object references, etc.

Reasoning foundationally, when names have structure, name equality becomes a computation; but, if our theory of interaction is to provide a basis for a theory of computation - especially of *distibuted* computation - then certainly this computation must be accounted for as well.

### Overview and contributions
The introduction of a *process constructor to dynamically convert a porcess into its code* is essential to obtain computational completeness, and simultaneously supplants the function of the `nu` operator (a compositional encoding of the `nu` operator into the calculus is given in [A Reflective High-Order Calculus](https://www.sciencedirect.com/science/article/pii/S1571066105051893).

Hennessey-Milner logic for `rho`-calculus is a *spatial logic* with operators detecting structural as well as behavioral content of of processes. The additional reflective structure on names gives rise to a new class of formulae denoting sets of *names*, referred to in the sequel as **namespaces**, hence the name *namespace logic*.

These new formulae suggest approaches to various application domains, e.g. reasoning about security, or the structure of data passed between processes, that differ somewhat from the current treatment of these domains using message-passing calculi. Properties are expressed as *formulae*, not as process specifications, thus observance is measured by *satisfaction*, not protocol equivalence.

The real contribution manifest by the logic is an instrument to better frame and sharpen those questions. These questions include the calculation of name equality in substitution versus synchronization.

## The calculus
We let `P`, `Q`, `R` range over processes and `x`, `y`, `z` range over names.
```
    P,Q ::= 0           // null process
          | x(y).P      // input
          | x!(P)       // lift
          | *x          // drop
          | P|Q         // parallel

    x,y ::= @P          // quote
```

#### Quote
The `pi`-calculus is parametric in a theory of names, i.e. there is no production for names, they are taken as terminals in the grammar. This is the first departure from a more standard presentation of an asynchronous mobile process calculus. A language production for names is included in the grammar. A name is a  *quoted* process, `@P`.

#### Parallel
This constructor is the usual parallel composition, denoting concurrent execution of the composed processes.

#### Lift and Drop
Despite the fact that names are built from (the code of) processes, we still maintain a distinction between processes and names. So if one wants to be able to generate a name from a given process, there must be a *process* constructor for a term that creates a name from a process. This is the motivation for the production `x!(P)`, dubbed here the *lift* operator. The intuitive meaning of this term is that the process `P` will be packaged up as its code, `@P`, and made available as an output on the port `x`.

`@P` is *impervious to substitution*. In `rho`-calculus, substitution does not affect the quoted process body! On the other hand, `x!(P)` is susceptible to substitution and as such constitutes a dynamic form of quoting because a substitution may change the process body before it is quoted, depending on the context in which `x!(P)` occurs.

Since names are quoted processes, we need a way to evaluate such an entity. The operator `*x`, *drop* `x`, (eventually) extracts the underlying process from the name. We say eventually because *this extraction only happens when a quoted process is substituted into this expression* (semantic substitution). As a consequence, the process `*x` is inert except under an input-prefix, i.e. when it's in a substitution context.

#### Input and Output
The input constructor is standard for an asynchronous name-passing calculus. Input blocks its continuation from execution until it receives a communication. Lift is a form of output which has no continuation because the calculus is asynchronous. It affords a convenient form of syntactic sugar.
```
    x[y] := x!(*y)
```

#### Null Process
The null process provides the sole atom out of which all processes (and the names they use) arise in much the same way that the natural numbers are constructed from `0`; or how all sets in ZF-set theory are constructed from the empty set; or how all games in Conway's theory of games and numbers are constructed from the empty game.

### Free and Bound Names
The *free names* of a process `P`, `FN(P)`, is a set defined recursively by
```
    FN( 0      ) = \emptyset
    FN( x(y).P ) = {x} \cup ( FN(P) \ {y} )
    FN( x!(P)  ) = {x} \cup FN(P)
    FN( P | Q  ) = FN(P) \cup FN(Q)
    FN( * x    ) = {x}
```
An occurrence of a name in a process is *bound* if it is not free. The set of all names (bound or free) occurring in the process `P` is denoted by `N(P)`.

## Logic
Namespace logic resides in the subfamily of Hennessey-Milner logics discovered by Caires and Cardelli known as *spatial logics*. As is seen below, in addition to the action modalities, we find formulae for *separation*, corresponding, at the logical level, to the structural content of the parallel operator at the level of the calculus. Likewise, we have quantification over names.

There is a difference between spatial logics discovered heretofore and this one. In the calculus, we find no need for an operator corresponding to the `nu` construction. However, revelation in spatial logic, is a structural notion. It detects the declaration of a new name. No such information is available in the reflective calculus or namespace logic. The calculus and the logic can arrange that names are used in a manner consistent with their being declared new as in the `pi`-calculus, but it cannot detect the declaration itself. As seen from this perspective, revelation is a somewhat remarkable observation, as it seems to be about detecting the programmer's intent.

Reflective logic
```
    F,G ::= true               // verity
          | 0                  // nullity
          | ~F                 // negation
          | F & G              // conjunction
          | F | G              // separation
          | * b                // descent
          | a!(F)              // elevation
          | <a?b> F            // activity
          | rec X . F          // greatest fix point
          | \forall n : F . G  // quantification

      a ::= @ F                // indication
          | b                  // ...

      b ::= @ P                // nomination
          | n                  // ...
```

We let `PForm` denote the set of formulae generated by the `F`-production, `QForm` denote the set of formulae generated by the `a`-production and `V` denote the set of propositional variables used in the `rec` production.

The semantics of the logic are given in terms of sets of processes (and names). We need the notion of a *valuation* `v: V -> P(Proc)`, where `P(X)` is the powerset of the set `X`, and use the notation `v{S / X}` to mean
```
    v{S / X}(Y) = #if Y = X #then S #else v(Y) #fi
```

The meaning of formulae is given by two mutually recursive functions
```
    [[-]](-): PForm x [V -> P(Proc)] -> P(Proc)
    ((-))(-): QForm x [V -> P(Proc)] -> P(@Proc)
```

taking a formula of the appropriate type and a valuation, and returning a set of processes or names, respectively.

```
      [[ true  ]](v) = Proc
      [[   0   ]](v) = {P: P \equiv 0}
      [[  ~F   ]](v) = Proc \ [[F]](v)
      [[ F & G ]](v) = [[F]](v) \cap [[G]](v)
      [[ F | G ]](v) = {P: \exists P0, P1. P \equiv P0 | P1, P0 \in [[F]](v), P1 \in [[G]](v)}
      [[  * b  ]](v) = {P: \exists Q. P \equiv Q | *x, x \in ((b))(v)}
      [[ a!(F) ]](v) = {P: \exists P',Q. P \equiv Q | x!(P'), x \in ((a))(v), P' \in [[F]](v)}
      [[<a?b>F ]](v) = {P: \exists P',Q. P \equiv Q | x(y).P', x \in ((a))(v), \forall c. \exists z. P{z / y} \in [[F{c / b}]](v)}
      [[rec X.F]](v) = \cup {S \subset Proc: S \subset [[F]](v{S / X})}
[[\forall n:G.F]](v) = \cap_{x \in ((@G))(v)} [[F{x / n}]](v)
           ((@F))(v) = {x: x \equiv_N @P, P \in [[F]](v)}
           ((@P))(v) = {x: x \equiv_N @P}
```

We say that a process `P` witnesses a formula `F` (resp. a name `x` witnesses `@F`), written `P |= F` (resp. `x |= @F`), when `\forall v. P \in [[F]](v)` (resp. `\forall v. x \in ((@F))(v)`).

#### Theorem 1
```
    P ~ Q  <=> (\forall F. P |= F <=> Q |= F)
```
The processes `P`, `Q` are *bisimilar* if and only if for all formulae `F`, `P` *witnesses* `F` if and only if `Q` *witnesses* `F`.

### Controlling Access to Namespaces
Suppose that `@F` describes some namespace, i.e. a collection of names. We can insist that a process restrict its next input to names in that namespace by insisting that it witness the formula
```
    <@F?b>true & ~<@(~F)?b>true
```

which simply says that *the process is currently able to take input from a name in the namespace* `@F` *and is not capable of taking input from any name outside of the namespace*.

We can also limit a server to serving only names in `@F` throughout the lifetime of its behavior
```
    rec X. <@F?b>X & ~<@(~F)?b>true
```

This formula is representative of the functionality of a firewall, except that it is a *static* check. A process witnessing this formula will behave as if it is behind a firewall allowing only access to the ports in `@F` without the need for the additional overhead of the watchdog machinery.

### Validating the Structure of Data
Processes use names as messages as well as using them to govern synchronization. The next example considers a space of names that might be seen as well-suited to play the role of data, for their structure loosely mimics the infoset model of XML.
```
    F_info = @{ rec X. \forall m. m!(\forall n. 0 \/ n!(X) \/ rec Y. { \forall n'. <n'?b>{X \/ Y} } \/ { X | X }) }
```

This formula is essentially a recursive disjunction selecting names that are first of all rooted with an enclosing lift operator - reminiscent of the way an XML document has a single enclosing root; and then are either
* an empty 'document'; or
* an 'element'; or
* a sequence of documents each 'located' at an input action; or
* an unordered group.
