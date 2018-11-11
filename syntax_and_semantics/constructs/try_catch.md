# try/catch

A `try/catch` construct is used to try an unsafe block of code, and catch any errors.

```ruby
try {
    "foo".some_undefined_method
    say "not executed"
} catch { |type, msg|
    say "Caught '#{type}', with message: #{msg}"
}
say "continued executing"
```

Output:

```
Caught 'error', with message: Undefined method `String.some_undefined_method' [...]
continued executing
```

`die` can be used to re-throw the error in the `catch` block.

When an error is thrown in the `try` block, the block is stopped, and the `catch` block is executed with information about the error. Assuming an error is not re-thrown, execution continues as normal after the `try` and `catch`.
