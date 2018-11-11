# Die, Assert, and Warn

## Die and Warn

These statements are the two builtin ways of issuing diagnostics in Sidef.

`die` will print its string operand followed by the filename and line number from which it was called, and exit the program (unless it is caught inside a `try`) with a non-zero exit code.

`warn` will act similarly, except it will not cause the program to exit, unless the `-W` flag was given to `sidef`, in which case it is equal to `die`.

```ruby
warn "keeps running"
die "dies"
say "stops running"
```
gives

```
keeps running at -E line 1
dies at -E line 2
```

## Assert

Simple C-style expression tests, which may be used to write simple unit tests for a program.

* `assert(exp)` crash if `Bool(exp)` is `false`.
* `assert_eq(exp1, exp2)` crash if `exp1 != exp2`
* `assert_ne(exp1, exp2)` crash if `exp1 == exp2`

Using these within a production program's main code path is generally considered bad practise (i.e a lack of interest in edge cases), but they have minor legitimate uses in main code paths for checking that basic features of the system are intact.

`assert` is a statement like `say`, `die`, and `warn`:

```ruby
say assert(true)    # -> prints "true"
say assert true     # ==/==
say assert(1, 2, 3) # ==/==
say assert false    # -> prints assert(false) failed...
say assert_eq 1 1   # same as say(assert_eq(1)), 1; it fails
```

`assert` will accept many arguments and test only 1; `assert_*` will accept exactly two arguments and thus requires parentheses.

A failed `assert*` stops the program, and is an error catchable with `try`.
