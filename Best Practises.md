# Best Practises

# Branching Strategy
We like to keep it simple. Our overall goal is to move towards [Truck based development](https://trunkbaseddevelopment.com/). But this requires that we have a solid CD pipeline (whatever this means) and [feature flags](https://www.optimizely.com/optimization-glossary/feature-flags/) implemented. In the meantime, we loosely follow the [Github Flow](https://guides.github.com/introduction/flow/#:~:text=GitHub%20flow%20is%20a%20lightweight,Created%20with%20Snap) with two additional rules.

1. We have a `master/main` branch that is always release ready. This means it's stable and can always be deployed to production at any moment.
2. We cannot merge any feature branches until its deploy-ready.

# [SOLID](https://en.wikipedia.org/wiki/SOLID) Principles

1. [Single Responsibility Principle](https://en.wikipedia.org/wiki/Single-responsibility_principle)

   A class should only have a single responsibility, that is, only changes to one part of the software's specification should be able to affect the specification of the class


2. [Open-closed Principle](https://en.wikipedia.org/wiki/Open%E2%80%93closed_principle)

   Software entities should be open for extension, but closed for modification

3. [Liskov substitution principle](https://en.wikipedia.org/wiki/Liskov_substitution_principle)

  Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program.

4. [Interface segregation principle](https://en.wikipedia.org/wiki/Interface_segregation_principle)

  Many client-specific interfaces are better than one general-purpose interface.

5. [Dependency inversion principle](https://en.wikipedia.org/wiki/Dependency_inversion_principle)

  One should "depend upon abstractions, [not] concretions.
