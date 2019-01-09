# Namespace Logic for Rho-Calculus Notes

### Abstract
In [A Reflective High-Order Calculus]() it was observed that a theory like the `pi`-calculus, dependent on a theory of *names*, can be *closed*, through a mechanism of *quoting*, so that *quoted processes* provide the necessary notion of names. We expand on this theme by examining a Hennessey-Milner (HM) logic corresponding to an asynchronous message-passing calculus built on a notion of quoting. Like standard HM logics, the logic exhibits formulae corresponding to sets of processes, but a new class of formulae, corresponding to sets of names, also emerges. This feature provides for a number of interesting possible applications from security to data manipulation. Specifically, we illustrate formulae for controlling process response on ranges of names reminiscent  of a (static) constraint on port access in a firewall configuration. Likewise, we exhibit formulae in a names-as-data paradigm corresponding to validation for fragment of `XML Schema`.

## Introduction
Practically, whether we consider MAC/IP addresses, domain names, or URL's, it is clear that distributed computing is practiced, today, using names. 

Theoretically, nowhere in the tools available to the computer scientist is there a countably infinite set of *atomic* entities that might function as names. All such sets, e.g. the natural numbers, the set of strings of finite length on some alphabet, etc., are *generated* from a finite presentation, and as such the elements of these sets inherit *structure* from the generating procedure. This structure can be "forgotten", but comes to the fore when building *executable* models of these calculi.

The fact that the [`pi`-calculus]() is not a closed theory, but rather a theory dependent upon some theory of names is both enabling and limiting. Biztalk: tcp/ip ports, urls, object references, etc.

Reasoning foundationally, when names have structure, name equality becomes a computation; but, if our theory of interaction is to provide a basis for a theory of computation - especially of *distibuted* computation - then certainly this computation must be accounted for as well. 

### Overview and contributions
The introduction of a *process constructor to dynamically convert a porcess into its code* is essential to obtain computational completeness, and simulataneously supplants the function of the `nu` operator (a compositional encoding of the `nu` operator into the calculus is given in [A Reflective High-Order Calculus]()). 

Hennessey-Milner logic for `rho`-calculus is a *spatial logic* with operators detecting structural as well as behvioral content of of processes. The additional reflective structure on names gives rise to a new class of formulae denoting sets of *names*, referred to in the sequel as **namespaces**, hence the name *namespace logic*.

These new formulae suggest approaches to various application domains, e.g. reasoning about security, or the structure of data passed between processes, that differ somewhat from the current treatment of these domains using message-passing calculi. Properties are expressed as *formulae*, not as process specifications, thus observance is measured by *satisfaction*, not protocol equivalence. 

The real contribution manifest by the logic is an instrument to better frame and sharpen those questions. These questions include the calculation of name equality in substitution versus synchronization.

## The calculus

## Logic












