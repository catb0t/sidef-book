# for

The `for` construct it's very popular construct as well. It's usually used for iteration over collections or for counting.

The following loop counts from 0 to 9:

```ruby
for (var i = 0; i < 10; i++) {
    say i
}
```

Alternatively, using a simpler form of `for`:

```ruby
for (0 ..^ 9) { |i|
    say i
}
```

To iterate over an array, Sidef supports yet another form of the `for` loop:

```ruby
for i in [1,2,3,4] {
    say i
}
```