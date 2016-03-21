[1]: http://rosettacode.org/wiki/Statistics/Normal_distribution

# [Statistics/Normal distribution][1]

```ruby
define τ = Number.tau
 
func normdist (m, σ) {
    var r = sqrt(-2 * 1.rand.log)
    var Θ = (τ * 1.rand)
    r * Θ.cos * σ + m
}
 
var size = 100_000
var mean = 50
var stddev = 4
 
var dataset = size.of { normdist(mean, stddev) }
var m = (dataset.sum(0) / size)
say ("m: #{m}")
 
var σ = sqrt(dataset »**» 2 -> sum(0) / size - m**2)
say ("s: #{σ}")
 
var hash = Hash()
dataset.each { |n| hash{ n.round(0) } := 0 ++ }
 
var scale = (180 * stddev / size)
const subbar = < ⎸ ▏ ▎ ▍ ▌ ▋ ▊ ▉ █ >
 
for i in (hash.keys.map{.to_i}.sort) {
    var x = (hash{i} * scale)
    var full = x.int
    var part = (8 * (x - full))
    say (i, "\t", '█' * full, subbar[part])
}
```

#### Output:
```
m: 49.99538275618550306540055142077589
s: 4.00295544816687358837821680496471
33      ⎸
34      ⎸
35      ⎸
36      ▏
37      ▎
38      ▊
39      █▋
40      ███▏
41      ██████▏
42      █████████▍
43      ███████████████▌
44      ███████████████████████▋
45      ████████████████████████████████▍
46      ████████████████████████████████████████████▎
47      █████████████████████████████████████████████████████▍
48      ███████████████████████████████████████████████████████████████▍
49      █████████████████████████████████████████████████████████████████████▌
50      ████████████████████████████████████████████████████████████████████████▋
51      █████████████████████████████████████████████████████████████████████▊
52      ██████████████████████████████████████████████████████████████▏
53      ████████████████████████████████████████████████████▉
54      ███████████████████████████████████████████▉
55      █████████████████████████████████▎
56      ███████████████████████⎸
57      ███████████████▋
58      █████████▋
59      █████▍
60      ███▍
61      █▊
62      ▋
63      ▍
64      ▏
65      ⎸
66      ⎸
```