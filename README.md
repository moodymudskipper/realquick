
<!-- README.md is generated from README.Rmd. Please edit that file -->

# realquick

A placeholder at the moment.

We want :

- `realquick::describe()` for one line summaries of objects, mentioning
  type, class, length if relevant, the namespace for a closure, this
  kind of things.
  - The default approach ignores the data content
  - An optional approach uses some of the content if we have enough room
    (as given by a `width` parameter), for instance it might include
    factor levels, missing values, function args… We can set them
    individually.
- `realquick::compare()` for one line comparison summaries.
  - We might use `waldo::compare(,max_diffs = 1)` and trim down the
    output if necessary, but it’s expensive since waldo seems not to
    return early when `max_diffs` are exceeded, and this package could
    be made dependency free.
- `realquick::assess(object, predicate, ptype)` describes the object
  only if predicate is not satisfied, and the description is limited to
  what differs from the prototype
- We use S3 methods and provide a mechanism for users to override them
  (we need this for {constructive} too)

Names are simple and meant to be used with the `namespace::notation`, no
need to worry about overriding common names.

All these functions return a string with a class that prints nice, so
they can easily be used with `stop()`, `abort()`, `warn()`.

We might provide an `action` parameter to these functions to trigger
`abort`, `warn`, `inform`, but our default behavior is low level, so
we’re not primarily an assertion package. Action takes a function but we
can provide a formula so we can pass additional args to `abort` this
way.

## Alternatives

`pillar::type_sum()` and `vctrs::vec_ptype_abbr().` provide very short
summaries to be used for column names, what we want is succinct
summaries to be used in messages, warnings, errors.

Some packages like {skimr} provide summaries, but these are not one
liners and generally too long to be integrated in a message.

{waldo} doesn’t export anything for short summaries but they do produce
them so we might want to check that code.

`constructive:::describe()` is a starting point.
