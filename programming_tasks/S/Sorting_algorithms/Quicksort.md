[1]: http://rosettacode.org/wiki/Sorting_algorithms/Quicksort

# [Sorting algorithms/Quicksort][1]

```ruby
func quicksort (a) {
    a.len < 2 && return(a);
    var p = a.popRand;          # to avoid the worst cases
    __FUNC__(a.grep{ .< p}) + [p] + __FUNC__(a.grep{ .>= p});
}
```