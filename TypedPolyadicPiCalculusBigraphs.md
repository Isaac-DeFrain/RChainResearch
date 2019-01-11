# Typed Polyadic Pi Calculus in Bigraphs

#### Abstract
*Bigraphs* have been introduced with the aim to provide a topographical meta-model for mobile, distributed agents that can manipulate their own communication links and nested locations.

> Examine a presentation of type systems on bigraphical systems using the notion of sorting. 

## Introduction
*Bigraphical reactive systems (BRS)* have been proposed as a topographical meta-model for mobile, distributed agents that can manipulate their own communication linkage and nested locations. Bigraphs generalize both the link structure characteristic of the `pi`-calculus and the nested location structure characteristic of the calculus of mobile ambients. A *bigraph* consists of two overlapping structures: a *place graph* and a *link graph*.

* Place graph: tuple of unordered trees that represents the topology of the system. Its *roots* contain nodes which represent locations or process constructors. Some leaves may be *sites* to be filled by other bigraphs, so giving rise to *bigraphical (multi-hole) contexts*. Each node is typed with a *control* which prescribes its number of *ports*. 

* Link graph: represents the system's connectivity. It links together ports and names in the bigraph's inner and outer interfaces. Names in the inner interface represent connection points offered to bigraphs that may fill sites; those in the outer interface represent the free names exported by the system.

*Binding bigraphs* extend this basic structure - known as pure bigraphs - by allowing some of the ports of a node to be "binding", i.e. all other points linked to the port must lie inside the node. A binding port enforces the notion of scope in a bigraph's links, resembling usual notions of binders in `lambda`- and `pi`-calculus. 












