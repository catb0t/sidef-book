[1]: http://rosettacode.org/wiki/Hailstone_sequence

# [Hailstone sequence][1]

```ruby
func hailstone(n) {
    var a = [n];
    while (n > 1) {
        a.append(n = (n %% 2 ? n/2 : (3*n + 1)));
    };
    return a;
}
 
# The hailstone sequence for the number 27
var arr = hailstone(var nr = 27);
say "#{nr}: #{arr[0..3].to_s} ... #{arr[-4..-1].to_s} (#{arr.len})";
 
# The longest hailstone sequence for a number less than 100,000
var h = [0, 0];
99_999.times { |i|
    (var l = hailstone(i).len) > h[1] && (
        h = [i, l];
    );
};
 
printf("%d: (%d)\n", h...);
```