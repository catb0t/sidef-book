[1]: http://rosettacode.org/wiki/Faulhaber's_formula

# [Faulhaber's formula][1]

```ruby
func bernoulli_number((1))       { 1/2 }
func bernoulli_number({.is_odd}) { 0/1 }

func bernoulli_number(n) {

    var a = [];
    0.to(n).each { |m|
        a[m] = 1/(m + 1)
        m.downto(1).each { |j|
            a[j-1] = j*(a[j-1] - a[j])
        }
    }

    return a[0]
}

func faulhaber_s_formula(p) {

    var formula = gather {
        0.to(p).each { |j|
            take "(#{binomial(p+1, j) * bernoulli_number(j) -> as_rat})*n^#{p+1 - j}"
        }
    }

    formula.grep! { !.contains('(0)*') }.join!(' + ')

    formula -= /\(1\)\*/g
    formula -= /\^1\b/g

    "1/#{p + 1} * (#{formula})"
}

0.to(9).each { |p|
    printf("%2d: %s\n", p, faulhaber_s_formula(p))
}
```

#### Output:
```
f(0) = 1/1 * (n)
f(1) = 1/2 * (n^2 + n)
f(2) = 1/3 * (n^3 + (3/2)*n^2 + (1/2)*n)
f(3) = 1/4 * (n^4 + (2)*n^3 + n^2)
f(4) = 1/5 * (n^5 + (5/2)*n^4 + (5/3)*n^3 + (-1/6)*n)
f(5) = 1/6 * (n^6 + (3)*n^5 + (5/2)*n^4 + (-1/2)*n^2)
f(6) = 1/7 * (n^7 + (7/2)*n^6 + (7/2)*n^5 + (-7/6)*n^3 + (1/6)*n)
f(7) = 1/8 * (n^8 + (4)*n^7 + (14/3)*n^6 + (-7/3)*n^4 + (2/3)*n^2)
f(8) = 1/9 * (n^9 + (9/2)*n^8 + (6)*n^7 + (-21/5)*n^5 + (2)*n^3 + (-3/10)*n)
f(9) = 1/10 * (n^10 + (5)*n^9 + (15/2)*n^8 + (-7)*n^6 + (5)*n^4 + (-3/2)*n^2)
```