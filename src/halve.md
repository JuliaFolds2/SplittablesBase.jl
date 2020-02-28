    SplittablesBase.halve(collection) -> (left, right)

Split `collection` (roughly) in half.

# Examples
```jldoctest
julia> using SplittablesBase: halve

julia> halve([1, 2, 3, 4])
([1, 2], [3, 4])
```

# Implementation

Implementations of `halve` on custom collections must satisfy
following laws.

(1) If the original collection is ordered, concatenating the
sub-collections returned by `halve` must be equivalent to the original
collection.  More precisely,

```julia
isequal(
    vec(collect(collection)),
    vcat(vec(collect(left)), vec(collect(right))),
)
```

must hold.

(2) `halve` must shorten the collection.  More precisely, if
`length(collection) > 1`, both `length(left) < length(collection)` and
`length(right) < length(collection)` must hold.

Furthermore, whenever implementable with cheap operations,
`length(left)` should be close to `length(collection) ÷ 2` as much as
possible.

# Supported collections

`halve` methods for following collections in `Base` are implemented in
SplittablesBase.jl:

* `AbstractArray`
* `AbstractString`
* `Tuple`
* `NamedTuple`
* `zip`
* `Iterators.partition`
* `Iterators.product`
* `Iterators.enumerate`

## Limitation

* `halve` on `zip` of iterators with unequal lengths does not satisfy
  the "`vcat` law".