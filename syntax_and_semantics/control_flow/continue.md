# continue

The `continue` statement can be used inside the `given/when` construct to jump to the next branch.

```ruby
var i = 10;
given (i) {
    when (10) {
        say "It's ten"
        continue
    }
    when (i.is_even) {
        say "It's even"
        continue
    }
    when (i % 5 == 0) {
        say "It's divisible by 5"
    }
}
```

#### Output:

```
It's ten
It's even
It's divisible by 5
```