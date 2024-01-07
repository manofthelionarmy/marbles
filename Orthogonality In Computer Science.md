[Links?](#)
[Embbed Videos?](#)
[Orthoganality - Wikipedia](https://en.wikipedia.org/wiki/Orthogonality)
# Summary

----
# Related Stuff

----
# Notes:
> Further information: [Orthogonality (programming)](https://en.wikipedia.org/wiki/Orthogonality_(programming) "Orthogonality (programming)") and [Orthogonal instruction set](https://en.wikipedia.org/wiki/Orthogonal_instruction_set "Orthogonal instruction set")

> Orthogonality in programming language design is the ability to use various language features in <mark style="background: #FFB86CA6;">arbitrary combinations with consistent results</mark>.[[6]](https://en.wikipedia.org/wiki/Orthogonality#cite_note-6) This usage was introduced by [Van Wijngaarden](https://en.wikipedia.org/wiki/Adriaan_van_Wijngaarden "Adriaan van Wijngaarden") in the design of [Algol 68](https://en.wikipedia.org/wiki/Algol_68 "Algol 68"):

> The number of independent primitive concepts has been minimized in order that the language be easy to describe, to learn, and to implement. On the other hand, these concepts have been applied “orthogonally” in order to maximize the expressive power of the language while trying to avoid deleterious superfluities.[[7]](https://en.wikipedia.org/wiki/Orthogonality#cite_note-7)

> Orthogonality is <mark style="background: #FFB86CA6;">a system design property</mark> which guarantees that modifying the technical effect produced by a component of <mark style="background: #FFB86CA6;">a system neither creates nor propagates side effects to other components of the system</mark>. Typically this is achieved through the [separation of concerns](https://en.wikipedia.org/wiki/Separation_of_concerns "Separation of concerns") and [encapsulation](https://en.wikipedia.org/wiki/Information_Hiding#Encapsulation "Information Hiding"), and it is essential for feasible and compact designs of complex systems. The emergent behavior of a system consisting of components should be controlled strictly by formal definitions of its logic and not by side effects resulting from poor integration, i.e., non-orthogonal design of modules and interfaces. Orthogonality reduces testing and development time because it is easier to verify designs that neither cause side effects nor depend on them.

- Meaning I can make changes that doesn't affect some other or all systems (i.e. in a system esign context).
- When I was reading this book for PostgreSQL, they mentioned that permissions/privileges for role creation are orthogonal, i.e. however you go about it when creating roles, you always get the same result (i.e. the combos/permutations for role creation.)
## Questions:

## Follow Up:
