[1]: http://rosettacode.org/wiki/Fibonacci_word

# [Fibonacci word][1]

```ruby
func entropy(s) {
    var counts = Hash.new;
    counts.default(0);
    s.each { |c| counts[c] += 1 };
    var e = 0;
    counts.values.each { |v|
        var freq = (v / s.len);
        e -= (freq * freq.log2);
    };
    return e;
}
 
var n_max = 37;
var words = ['1', '0'];
 
{
    words.append(words[-1] + words[-2]);
} * (n_max - words.len);
 
say ('%3s %10s %15s  %s' % %w[N Length Entropy Fibword]);
 
words.range.each { |i|
    var word = words[i];
    say ('%3i %10i %15.12f  %s' % [i+1,
                                   word.len,
                                   entropy(word),
                                   word.len<30 ? word : '<too long>']);
}
```
