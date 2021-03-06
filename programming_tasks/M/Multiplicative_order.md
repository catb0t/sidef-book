[1]: https://rosettacode.org/wiki/Multiplicative_order

# [Multiplicative order][1]

```ruby
func mo_prime(a, p, e) {
    var m  = p**e
    var t  = (p-1)*(p**(e-1))
    var qs = [1]
 
    for f in (t.factor_exp) {
        qs.map! {|q|
            0..f[1] -> map {|j| q * f[0]**j }...
        }
    }
 
    qs.sort.first_by {|q| powmod(a, q, m) == 1 }
}
 
func mo(a, m) {
    gcd(a, m) == 1 || die "#{a} and #{m} are not relatively prime"
    Math.lcm(1, m.factor_exp.map {|r| mo_prime(a, r...) }...)
}
 
say mo(37, 1000)
say mo(54, 100001)
 
with (10**20 - 1) {|b|
    say mo(2, b)
    say mo(17, b)
}
```

#### Output:
```
100
9090
3748806900
1499522760
```