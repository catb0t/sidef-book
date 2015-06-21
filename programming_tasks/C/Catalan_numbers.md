[1]: http://rosettacode.org/wiki/Catalan_numbers

# [Catalan numbers][1]

```ruby
func f(i) { i.isZero ? 1 : (i * f(i-1)) };
func c(n) { f(2*n) / f(n) / f(n+1) };
```


Recursive (with memoization):

```ruby
func c(n) {
    static mem = [1];
    mem[n-1] := (c(n-1) * (4 * n - 2) / (n + 1));
}
```


Calling the function:

```ruby
15.times { |i|
    say "#{i-1}\t#{c(i-1)}";
}
```

#### Output:
```
0       1
1       1
2       2
3       5
4       14
5       42
6       132
7       429
8       1430
9       4862
10      16796
11      58786
12      208012
13      742900
14      2674440
```