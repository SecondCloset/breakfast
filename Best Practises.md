# Best Practises

# Branching Strategy
We like to keep it simple. Our overall goal is to move towards [Truck based development](https://trunkbaseddevelopment.com/). But this requires that we have a solid CD pipeline (whatever this means) and [feature flags](https://www.optimizely.com/optimization-glossary/feature-flags/) implemented. In the meantime, we loosely follow the [Github Flow](https://guides.github.com/introduction/flow/#:~:text=GitHub%20flow%20is%20a%20lightweight,Created%20with%20Snap) with two additional rules.

1. We have a `master/main` branch that is always release ready. This means it's stable and can always be deployed to production at any moment.
2. We cannot merge any feature branches until its deploy-ready.

