[1]: https://rosettacode.org/wiki/Penrose_tiling

# [Penrose tiling][1]

Using the LSystem class defined at [Hilbert curve](https://rosettacode.org/wiki/Hilbert_curve#Sidef).

```ruby
var rules = Hash(
    a => 'cE++dE----bE[-cE----aE]++',
    b => '+cE--dE[---aE--bE]+',
    c => '-aE++bE[+++cE++dE]-',
    d => '--cE++++aE[+dE++++bE]--bE',
    E => '',
)
 
var lsys = LSystem(
    width:  1000,
    height: 1000,
 
    scale: 1,
    xoff: -500,
    yoff: -500,
 
    len:   40,
    angle: 36,
    color: 'dark blue',
)
 
lsys.execute('[b]++[b]++[b]++[b]++[b]', 5, "penrose_tiling.png", rules)
```


Output image: [Penrose tiling](https://github.com/trizen/rc/blob/master/img/penrose-tiling-sidef.png)