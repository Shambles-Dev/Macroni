## The Intuition

Macroni uses a dynamic effect system that limits the potential harm of mutation by limiting its observability.

These rules always apply:
* Variable names must be unique within the same scope (e.g. an immutable variable and a mutable variable cannot have the same name in the same scope).
* Inner scopes can shadow outer scopes.
* Immutable variables can only be bound to transitively immutable values.  They can be bound to non-first-class values.
* Immutable variables are lexically scoped.
* Mutable variables can store all first-class values.
* Mutable variables are not lexically scoped.
* Implementations of the same generic function must have the same mutability.


## Sandbox Boundaries




## Lexical Scope

`def-macro`

`def-fun`


## Module Scope

`mdef-mmfun`

imports

exports


## Type Scope

`def-type`

`def-mfun`

`thunk`


## Local Scope

`def`

`mdef`


## Interactions

continuations (mutability depends on call stack frames)
