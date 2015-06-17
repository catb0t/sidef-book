[1]: http://rosettacode.org/wiki/Sorting_algorithms/Stooge_sort

# [Sorting algorithms/Stooge sort][1]

```ruby
func stooge(x, i, j) {
    x[j] < x[i] && (
        x[i, j] = x[j, i];
    );
 
    j-i > 1 && (
        var t = ((j - i + 1) / 3);
        stooge(x, i,     j - t);
        stooge(x, i + t, j    );
        stooge(x, i,     j - t);
    );
}
 
var a = 20.of { 100.rand.int };
 
say "Before #{a}";
stooge(a, 0, a.offset);
say "After  #{a}";
```