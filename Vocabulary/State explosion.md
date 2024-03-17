 [[State explosion]]  is a problem in [Model-checking](Model-checking.md) that can occur if the system being verified has many components that make transitions in parallel. This leads to big computational costs.

  The parallel composition of two concurrent components is indeed modele by taking the [Cartesian Product](Cartesian%20Product) of the corresponding [state space](state%20space)s: The global [state space](state%20space) of a reactive system may grow ==exponentially== with the number of concurrent processes running in the system.

The expolorion of such a huge state space may be prohibitive even for an algorithm running in linear time in the size of the model.

