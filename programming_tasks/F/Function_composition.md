[1]: http://rosettacode.org/wiki/Function_composition

# [Function composition][1]

```ruby
func compose(f, g) {
    func(x) { f(g(x)) }.copy;
};
var fg = compose(func(x){Math.sin(x)}, func(x){Math.cos(x)});
say fg(0.5);   # => 0.7691963548410084218525147580510688880995
```