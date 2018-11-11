# Include and Import

These statements allow the organising of Sidef code into modules and files in a directory tree.

## Include

An `include` statement makes another Sidef module available in the current environment. Its first form searches Sidef's current working directory, and `perl5/share/sidef`<sup>1</sup> for a file with the module's name, and extension `.sm`. It creates an implicit [Module](syntax_and_semantics/modules.md), or re-binds an existing one, to contain the imported code.

```ruby
include another_module    # another_module.sm declares var A = 1
another_module::A         # -> 1
```

A module name to `include` might contain `::`, which indicates traversing a directory but not other modules.
If we have the files `./a.sm`, which contains `module b { var C = 1 }`, and `./a/b.sm` containing `var C = 1`, the `include` statement alone can only find the *file* `b.sm`, and not the *module* `b` in `a.sm`.

```ruby
include a    # -> 1
include a::b # -> 2
```

To access `a.sm`'s `b` module directly, use `import a::b` after `include a`.

The second, function-call form of `include` is C-style, including verbatim the content of another file into the current program at parse time.

```ruby
include("path/to/file.sf")
```

It cannot be used as a version of `eval` because it is unconditional (will be eagerly evaulated like a literal, regardless of position in the syntax tree), and it does not return any value, only making declared names visible.

<sup>1</sup>wherever Perl *would* find the Sidef module regardless of whether it's installed

## Import

An `import` statement is used to bring a module's names into the current namespace. The last `::`-delimited part of the `import` operand is the name to import.

<!--
document how to import multiple names at once, it is only vaguely mentioned in the wiki
scoping of imported names as well
-->

```ruby
module A { var F = 1 }

# can only access A::F here
say A::F

import A::F

say F # -> 1
```
