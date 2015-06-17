[1]: http://rosettacode.org/wiki/Statistics/Basic

# [Statistics/Basic][1]

```ruby
func generate_statistics(n) {
    var sum = (var sum2 = 0);
    var hist = 10.of(0);
 
    n.times {
        var r = 1.rand;
        sum += r;
        sum2 += r**2;
        hist[10 * r] += 1;
    };
 
    var mean = (sum / n);
    var stddev = Math.sqrt((sum2 / n) - mean**2);
 
    say "size: #{n}";
    say "mean:   #{mean}";
    say "stddev: #{stddev}";
 
    var max = hist.max;
    hist.range.each {|i|
        say ("%.1f:%s" % [0.1*i, "=" * (70*hist[i] / max)]);
    };
    print "\n";
}
 
[100, 1000, 10000].each {|n| generate_statistics(n) };
```