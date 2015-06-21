[1]: http://rosettacode.org/wiki/Nth_root

# [Nth root][1]

```ruby
func nthroot(n, a, precision=1e-5) {
  var x = 1;
  var prev = 0;
  while ((prev-x).abs > precision) {
    prev = x;
    x = (((n-1)*prev + a/(prev**(n-1))) / n);
  };
  return x;
}
 
say nthroot(5,34);  # => 2.024397458501034082599817835297912829678
```