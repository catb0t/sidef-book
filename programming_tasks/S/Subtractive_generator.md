[1]: http://rosettacode.org/wiki/Subtractive_generator

# [Subtractive generator][1]

```ruby
class SubRandom(seed) {
 
    def state = [];
    const mod = 1_000_000_000;
 
    method new {
        var s = [seed % mod, 1];
        53.times {
            s.append((s[-2] - s[-1]) % mod);
        };
        state = range(s).map {|i| s[(34 + 34*i) % 55] };
        range(55, 219).each { self.subrand };
    }
 
    method subrand {
        var x = ((state.shift - state[-24]) % mod);
        state.append(x);
        return x;
    }
}
 
var r = SubRandom(292929);
10.times { say r.subrand };
```

#### Output:
```
467478574
512932792
539453717
20349702
615542081
378707948
933204586
824858649
506003769
380969305
```